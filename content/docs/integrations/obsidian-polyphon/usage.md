---
title: "Usage"
weight: 30
description: "How to use the Polyphon sidebar in Obsidian — selecting compositions, sending messages, and reading responses."
---

## Opening the sidebar

Open the Polyphon sidebar any time from:

- The **message square** icon in the Obsidian ribbon (left edge)
- The command palette: `Cmd/Ctrl+P → Polyphon: Open sidebar`

The sidebar docks into Obsidian's right panel. You can drag it to any panel position like any other Obsidian view.

---

## Sending a message

1. Select a composition from the **dropdown** at the top of the sidebar — this determines which voices will respond
2. Type your message in the input field at the bottom
3. Press **Send** or `Enter` to submit (`Shift+Enter` inserts a newline)

Polyphon routes the message to every voice in the composition. Each voice's response streams in as it arrives, labeled by voice name.

---

## Reading responses

Responses appear in a unified conversation thread, with each voice's reply clearly labeled. Voices respond in parallel — you'll see multiple responses streaming simultaneously for compositions with more than one voice.

If a composition has continuation enabled, voices will automatically respond in subsequent rounds without needing another message from you.

---

## Active file context

When you send the first message of a session, the plugin automatically prepends the path of your currently open file. This gives the voices immediate context about what you're working on without you having to describe it. If no file is open, no path is added.

---

## Mentions

You can direct a message to a specific voice by mentioning it by name using `@VoiceName`. The message is sent only to that voice rather than broadcast to the full composition.

---

## Reconnecting

If Polyphon is restarted while the sidebar is open, the plugin will attempt to reconnect automatically. You can also force a reconnect by closing and reopening the sidebar.
