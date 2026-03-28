---
title: "Getting Started"
weight: 10
description: "Install the Polyphon VS Code extension and connect it to your running Polyphon instance."
---

The Polyphon extension for VS Code lets you run multi-voice AI conversations directly from your editor. It connects to a running Polyphon desktop instance over the TCP API, giving you access to your compositions and voice configurations without leaving VS Code — with full awareness of your open file, selection, and diagnostics.

---

## Requirements

- **Polyphon** must be installed and running — [download it here](https://polyphon.ai/#download)
- **VS Code 1.85** or later
- The Polyphon TCP API server must be reachable (it runs on `127.0.0.1:7432` by default)

---

## Installation

### VS Code Marketplace

Search for **Polyphon** in the Extensions panel (`Cmd/Ctrl+Shift+X`), or install directly from the [VS Code Marketplace](https://marketplace.visualstudio.com/items?itemName=polyphon-ai.vscode-polyphon).

### Manual installation (VSIX)

1. Download the `.vsix` from the [latest release](https://github.com/polyphon-ai/vscode-polyphon/releases/latest)
2. In VS Code: **Extensions** → **⋯** → **Install from VSIX…**
3. Select the downloaded file
4. Reload VS Code when prompted

---

## First launch

1. Start Polyphon on your machine
2. Click the **Polyphon** icon in the Activity Bar, or run **Polyphon: New Session** from the Command Palette (`Cmd/Ctrl+Shift+P`)
3. The Polyphon panel opens in the sidebar
4. If the connection succeeds, the composition dropdown will populate with your saved compositions

If the panel shows a connection error, confirm Polyphon is running and check the [configuration](../configuration/) to make sure the host, port, and API token are correct.
