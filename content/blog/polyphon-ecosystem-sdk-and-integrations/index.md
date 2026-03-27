---
title: "The Polyphon Ecosystem: SDK, CLI, and Obsidian Plugin"
description: "Polyphon started as a desktop app for multi-voice AI conversations. With the launch of the @polyphon-ai/js SDK, the poly CLI, and the obsidian-polyphon plugin, it is becoming a programmable platform whose compositions and sessions follow you across your tools."
date: "2026-03-27T02:23:00-0400"
draft: false
tags: ["sdk", "ecosystem", "obsidian", "cli", "multi-agent", "announcement"]
categories: ["Announcements", "Product", "Developers"]
image: "polyphon-ecosystem-sdk-and-integrations.webp"
aliases: ["/posts/polyphon-ecosystem-sdk-and-integrations/"]
---

{{< figure-float src="polyphon-ecosystem-sdk-and-integrations.webp" alt="Glowing amber sphere connected by luminous blue circuit pathways to three laptop terminals on dark navy background." >}}

## The real product was never just the window on your screen.

The interesting part was the workflow behind it: a persistent composition of voices, a shared conversation, and a way to return to that conversation from wherever your work actually happens. Sometimes that is the desktop app. Sometimes it is a shell script. Sometimes it is the note you already have open in Obsidian.

Polyphon's next step is not another isolated feature. It is the same system becoming available through three new entry points: the **`@polyphon-ai/js` SDK**, the **`poly` CLI**, and the **`obsidian-polyphon`** plugin.

## One engine, multiple surfaces

The desktop app remains where most people will create compositions, tune voices, and configure providers. But once Polyphon is running, it exposes a local API that other clients can connect to.

That changes the shape of the product in an important way. The intelligence lives in the shared system, not in any single client. A session you start from the terminal shows up in the desktop app. A session you resume in Obsidian uses the exact composition you built earlier. Your compositions and sessions are no longer trapped inside one interface — they follow you across the tools where your work actually happens.

## The SDK: `@polyphon-ai/js`

```sh
npm install @polyphon-ai/js
```

`@polyphon-ai/js` is a typed TypeScript client for the Polyphon API. It removes the socket-management work so you can script workflows against Polyphon instead of rebuilding client plumbing.

```ts
import { PolyphonClient, readLocalToken } from '@polyphon-ai/js';

const client = new PolyphonClient({
  token: readLocalToken(), // reads from ~/Library/Application Support/Polyphon/api.key
});

await client.connect();

const compositions = await client.compositions();
const session = await client.createSession(compositions[0].id, 'release-script');

await client.broadcast(
  { sessionId: session.id, content: 'Summarize the trade-offs in this draft.' },
  ({ voiceName, delta }) => process.stdout.write(delta),
);

client.disconnect();
```

`readLocalToken()` finds the authentication key Polyphon writes to your app data directory automatically — no manual token setup required for local use.

The API surface covers compositions, sessions, broadcast and directed prompts, streaming deltas, session export, message search, and provider status. The SDK version always matches the Polyphon app version: install `@polyphon-ai/js@0.13.x` for Polyphon `0.13.x`. For testing, `@polyphon-ai/js/testing` exports `MockPolyphonServer` — a full in-process server that speaks the wire protocol, so you can test your integration without a running desktop app in CI.

## The CLI: `poly`

```sh
npm install -g @polyphon-ai/poly
```

`poly` is for the moments when opening the full app is unnecessary friction. It is also built entirely on `@polyphon-ai/js` — the first production consumer of the SDK — which makes it a useful proof that the SDK works well for real integrations.

```sh
# Confirm Polyphon is reachable
poly status

# List saved compositions
poly compositions list

# Create a session, then run a prompt and stream the response
SESSION=$(poly sessions new --composition <id> --format json | jq -r '.id')
poly run --session $SESSION --prompt "$(git diff HEAD~1)" --stream
```

`poly run` broadcasts to all voices in the session. `poly ask` directs a message to a specific voice. Both support `--stream` for live token output and `--format json` for structured output you can pipe elsewhere.

Named remotes and environment variables let `poly` reach a Polyphon instance running on a different machine:

```sh
poly remote add home-server --host 192.168.1.10 --token-file ~/.polyphon/home.key
poly --remote home-server compositions list
```

This makes it practical to keep Polyphon running on the machine you prefer and control it from anywhere.

## The Obsidian Plugin: `obsidian-polyphon`

The Obsidian plugin is the clearest example of why shared state matters — and probably the most immediately legible one for people who do not write scripts.

Plenty of people think with AI in one place and write in another. That context switching adds up. `obsidian-polyphon` brings a Polyphon conversation into the Obsidian sidebar, so the discussion can happen alongside the note you are already working in.

Once connected to your running Polyphon instance, the plugin lets you choose a composition, create or resume a session, and send prompts. Multi-voice responses stream into the sidebar with each voice labeled. What makes this feel different from configuring a new AI integration is that you are using the same compositions you already built in Polyphon. The voices, the tones, the system prompt templates, the conductor profile — all of it carries over. You are not setting up a new AI tool. You are bringing the one you already have into your notes.

The practical pattern: keep a live multi-voice discussion beside a draft, a meeting note, or a research document, without switching windows.

## Three ways into the same system

Taken together, these three launches reflect what Polyphon is becoming. Each one maps to a distinct job:

- **SDK**: build something new — scripts, automations, internal tools
- **CLI**: automate or script what you already do, without writing a full application
- **Obsidian plugin**: bring the conversation into the writing environment where you already think

Configure in the app. Script from the terminal. Think in your vault. Return to the desktop UI when you want the full visual context. It is one underlying conversation model — not three separate products.

## A few places to start

- Pipe `git diff HEAD~1` into `poly run --stream` with a composition tuned for code review, before you open a pull request.
- Turn a recurring multi-voice prompt workflow into a small Node.js script with the SDK — five to ten lines with streaming handled.
- Open the Obsidian plugin alongside a draft you are actively working on and keep the conversation in view while you write.

The API reference is at [polyphon.ai/docs/for-developers/api](/docs/for-developers/api). The SDK source is at [polyphon-ai/polyphon-js](https://github.com/polyphon-ai/polyphon-js). The Obsidian plugin is at [polyphon-ai/obsidian-polyphon](https://github.com/polyphon-ai/obsidian-polyphon).

**[Download Polyphon](https://polyphon.ai/#download)** — everything else connects to it.

---

*Where would you bring Polyphon first: into your scripts, your notes, or something else entirely?*
