---
title: "Configuration"
weight: 20
description: "Configure the Polyphon VS Code extension — connection settings and API token."
---

Open **Settings** (`Cmd/Ctrl+,`) and search for `polyphon` to configure the extension.

---

## Connection

| Setting | Default | Description |
|---------|---------|-------------|
| `polyphon.host` | `127.0.0.1` | Hostname or IP address of the machine running Polyphon |
| `polyphon.port` | `7432` | TCP port the Polyphon API server is listening on |
| `polyphon.token` | _(empty)_ | Authentication token for the Polyphon API |

For a local setup you won't need to change the host or port. If Polyphon is running on a different machine on your network, set the host to that machine's IP address.

---

## API token

Polyphon requires an API token to accept connections. The token is generated when Polyphon first runs and stored at:

- **macOS**: `~/Library/Application Support/Polyphon/api.key`

The easiest way to set the token is to run **Polyphon: Read Local API Token** from the Command Palette — this reads the key file from the default location and fills it in automatically. You can also paste the token manually in Settings.

---

## Status bar

The extension shows a connection indicator in the VS Code status bar (bottom right):

| Indicator | Meaning |
|-----------|---------|
| `$(radio-tower) Polyphon` | Connected |
| `$(sync~spin) Polyphon` | Connecting |
| `$(debug-disconnect) Polyphon` | Disconnected |
| `$(error) Polyphon` | Connection error |

Click the status bar item to open the Polyphon panel.
