---
title: "Getting Started"
weight: 10
description: "Install the Polyphon Obsidian plugin and connect it to your running Polyphon instance."
---

The Polyphon plugin for Obsidian lets you run multi-voice AI conversations directly from your vault. It connects to a running Polyphon desktop instance over the TCP API, giving you access to your compositions and voice configurations without leaving Obsidian.

---

## Requirements

- **Polyphon** must be installed and running — [download it here](https://polyphon.ai/#download)
- **Obsidian desktop** — the plugin is desktop-only; mobile is not supported
- The Polyphon TCP API server must be reachable (it runs on `127.0.0.1:7432` by default)

---

## Installation

The plugin is not yet listed in the Obsidian community plugin directory. Install it manually or via BRAT.

### Manual installation

1. Download the latest release from the [obsidian-polyphon releases page](https://github.com/polyphon-ai/obsidian-polyphon/releases) — you need `main.js`, `manifest.json`, and `styles.css`
2. In your vault, create the folder `.obsidian/plugins/polyphon/` if it doesn't exist
3. Copy the three files into that folder
4. Open Obsidian **Settings → Community plugins**, disable Safe mode if prompted, and enable **Polyphon**

### BRAT (automatic updates)

[BRAT](https://github.com/TfTHacker/obsidian42-brat) is a community plugin that lets you install and auto-update plugins not yet in the official directory.

1. Install BRAT from the Obsidian community plugin directory
2. In BRAT settings, click **Add Beta plugin** and enter `polyphon-ai/obsidian-polyphon`
3. BRAT installs the plugin and keeps it up to date automatically

---

## First launch

1. Start Polyphon on your machine
2. Click the **message square** icon in the Obsidian ribbon, or run `Cmd/Ctrl+P → Polyphon: Open sidebar`
3. The Polyphon sidebar opens in the right panel
4. If the connection succeeds, the composition dropdown will populate with your saved compositions

If the sidebar shows a connection error, confirm Polyphon is running and check the [configuration](./configuration/) to make sure the host, port, and API token are correct.
