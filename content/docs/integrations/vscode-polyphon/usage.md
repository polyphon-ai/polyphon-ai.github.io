---
title: "Usage"
weight: 30
description: "How to use the Polyphon panel in VS Code — selecting compositions, attaching code context, and reading responses."
---

## Opening the panel

Open the Polyphon panel any time from:

- The **Polyphon** icon in the Activity Bar (left edge)
- The Command Palette: `Cmd/Ctrl+Shift+P → Polyphon: New Session`

The panel docks into the VS Code sidebar. You can drag it to any panel position like any other VS Code view.

---

## Sending a message

1. Select a composition from the **dropdown** at the top of the panel — this determines which voices will respond
2. Type your message in the input field at the bottom
3. Press **Send** or `Enter` to submit (`Shift+Enter` inserts a newline)

Polyphon routes the message to every voice in the composition. Each voice's response streams in as it arrives, labeled by voice name.

---

## Reading responses

Responses appear in a unified conversation thread, with each voice's reply clearly labeled. Voices respond in parallel — you'll see multiple responses streaming simultaneously for compositions with more than one voice.

---

## Code context

Click **📎 attach context** before sending to include information from your editor:

- **Active file** — the path of your currently open file
- **Selection** — any selected text, included as a fenced code block
- **Diagnostics** — active error diagnostics within your selected range (up to 5)

The context is prepended to the message sent to Polyphon. Only your plain message text is shown in the conversation panel — the context is invisible in the UI but present in what the voices receive.

---

## Right-click menu

Select code in the editor, right-click, and choose **Polyphon: Ask About Selection** to open the panel with your selection pre-filled in the input field.

---

## Mentions

You can direct a message to a specific voice by mentioning it by name using `@VoiceName`. Type `@` to see a dropdown of voices in the current composition. Selecting one sends your message only to that voice rather than broadcasting to the full composition.

---

## Commands

| Command | Description |
|---------|-------------|
| **Polyphon: Connect** | Manually connect to Polyphon |
| **Polyphon: Disconnect** | Disconnect from Polyphon |
| **Polyphon: New Session** | Create a new session in the active composition |
| **Polyphon: Ask About Selection** | Open the panel with the current selection pre-filled |
| **Polyphon: Read Local API Token** | Auto-populate the API token from the running Polyphon instance |

---

## Reconnecting

If Polyphon is restarted while the panel is open, the extension will attempt to reconnect automatically every 5 seconds. You can also force a reconnect using **Polyphon: Connect** from the Command Palette.
