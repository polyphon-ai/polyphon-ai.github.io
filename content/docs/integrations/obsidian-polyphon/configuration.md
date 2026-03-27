---
title: "Configuration"
weight: 20
description: "Configure the Polyphon Obsidian plugin — connection settings, API token, and options."
---

Open **Settings → Polyphon** to configure the plugin.

---

## Connection

| Setting | Default | Description |
|---------|---------|-------------|
| Host | `127.0.0.1` | Hostname or IP address of the machine running Polyphon |
| Port | `7432` | TCP port the Polyphon API server is listening on |
| API token | _(empty)_ | Authentication token for the Polyphon API |

For a local setup you won't need to change the host or port. If Polyphon is running on a different machine on your network, set the host to that machine's IP address.

---

## API token

Polyphon requires an API token to accept connections. The token is generated when Polyphon first runs and stored at:

- **macOS**: `~/Library/Application Support/Polyphon/api.key`

The easiest way to set the token is to click **Read local token** in the plugin settings — this reads the key file from the default location and fills it in automatically. You can also paste the token manually if needed.

---

## Options

| Setting | Default | Description |
|---------|---------|-------------|
| Persist conversations | Off | Save conversation history to Obsidian's plugin data and restore it when you reopen the sidebar |
| Debug mode | Off | Log raw JSON-RPC frames to the browser console — useful for troubleshooting connection issues |
