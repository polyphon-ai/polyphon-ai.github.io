---
title: "JavaScript SDK"
description: "Control Polyphon from Node.js and TypeScript scripts using the official @polyphon-ai/js client library."
weight: 11
---

## Overview

`@polyphon-ai/js` is the official TypeScript client for the Polyphon TCP API. It wraps every API method with full TypeScript types and handles connection management, request/response matching, and streaming chunks.

The SDK runs in **Node.js only** — it communicates over TCP and has no browser support.

## Installation

```bash
npm install @polyphon-ai/js
```

Requires Node.js 20 or later.

## Quick start

```typescript
import { PolyphonClient, readLocalToken } from '@polyphon-ai/js';

const client = new PolyphonClient({ token: readLocalToken() });
await client.connect();

// List compositions and start a session from the first one
const [composition] = await client.compositions();
const session = await client.createSession(composition.id, 'sdk');

// Broadcast a message and stream the response tokens
await client.broadcast(
  { sessionId: session.id, message: 'Summarise the latest news in AI.' },
  (chunk) => process.stdout.write(chunk.token),
);

client.disconnect();
```

## Authentication

Polyphon writes its API token to `~/Library/Application Support/Polyphon/api.key` when the TCP server is enabled. The `readLocalToken()` helper reads it automatically:

```typescript
import { readLocalToken } from '@polyphon-ai/js';

const token = readLocalToken(); // throws if Polyphon is not running
```

You can also pass a token directly:

```typescript
const client = new PolyphonClient({
  token: process.env.POLYPHON_TOKEN!,
  host: '127.0.0.1', // default
  port: 7432,        // default
});
```

## Connecting

```typescript
await client.connect();   // opens the TCP socket and authenticates
client.disconnect();      // closes the socket
client.getState();        // 'idle' | 'connecting' | 'connected' | 'disconnected'
```

`connect()` opens the TCP socket. Authentication happens automatically on the first call using the token you provided.

## Compositions

```typescript
// List all compositions
const compositions = await client.compositions();
const archived = await client.compositions({ includeArchived: true });

// Get a single composition
const composition = await client.getComposition({ id });

// Create, update, delete, archive
const created = await client.createComposition({ name, voices });
const updated = await client.updateComposition({ id, name, voices });
await client.deleteComposition({ id });
await client.archiveComposition({ id });
```

## Sessions

```typescript
// List sessions
const sessions = await client.sessions();
const forComposition = await client.sessions({ compositionId });

// Get, create, delete, rename, archive
const session = await client.getSession({ id });
const newSession = await client.createSession(compositionId, 'sdk');
await client.deleteSession({ id });
await client.renameSession({ id, name: 'New name' });
await client.archiveSession({ id });

// Fetch messages in a session
const messages = await client.getMessages({ sessionId: session.id });

// Export a session transcript
const { content } = await client.exportSession({ id, format: 'markdown' });
```

## Sending messages

### Broadcast

Send a message to all voices in a session simultaneously:

```typescript
const result = await client.broadcast({ sessionId, message: 'Hello' });
```

### Broadcast with streaming

Pass an `onChunk` callback to receive tokens as they arrive:

```typescript
await client.broadcast(
  { sessionId, message: 'Explain quantum entanglement.' },
  (chunk) => {
    process.stdout.write(chunk.token);
  },
);
```

The callback receives `{ voiceId, voiceName, token, sessionId }` for each streamed token.

### Ask a specific voice

Send a message to one voice by name:

```typescript
await client.ask(
  { sessionId, message: 'What do you think?', voiceName: 'Claude' },
  (chunk) => process.stdout.write(chunk.token),
);
```

### Abort

```typescript
await client.abort({ sessionId });
```

## Search

```typescript
const { messages } = await client.searchMessages({ query: 'quantum', limit: 20 });
```

## Status and profile

```typescript
const status = await client.getApiStatus();
const providers = await client.getProviderStatus();
const profile = await client.getUserProfile();
```

## Error handling

All methods throw an `RpcError` on API-level failures:

```typescript
import { RpcError } from '@polyphon-ai/js';

try {
  await client.getSession({ id: 'nonexistent' });
} catch (err) {
  if (err instanceof RpcError) {
    console.error(err.code, err.message); // e.g. -32001, 'Session not found'
  }
}
```

See the [TCP API reference](../api/) for the full list of error codes.

## Testing

The SDK ships a `MockPolyphonServer` you can use in tests without a running Polyphon instance:

```typescript
import { MockPolyphonServer } from '@polyphon-ai/js/testing';
import { PolyphonClient } from '@polyphon-ai/js';

let server: MockPolyphonServer;
let client: PolyphonClient;

beforeEach(async () => {
  server = new MockPolyphonServer();
  await server.listen();
  client = new PolyphonClient({ token: server.token, port: server.port });
  await client.connect();
});

afterEach(async () => {
  client.disconnect();
  await server.close();
});

test('lists compositions', async () => {
  const compositions = await client.compositions();
  expect(compositions).toHaveLength(1); // MockPolyphonServer seeds one composition
});
```

`MockPolyphonServer` seeds a composition, a session, and sample messages. See `@polyphon-ai/js/testing` for the full fixture set.

## Further reading

- [TCP API Server reference](../api/) — full method listing, wire protocol, error codes
- [MCP Server](../mcp/) — expose Polyphon as a tool to any MCP-compatible AI client
- [poly CLI](../../polyphon/poly/) — command-line access to the same TCP API
