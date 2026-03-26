---
title: "Polyphon v0.12.0 Released"
description: "Polyphon v0.12.0 is now available for download."
date: "2026-03-26T21:35:58Z"
draft: false
tags: ["release", "announcement"]
categories: ["Announcements"]
---

**What's New**
- Each voice in a composition can now have its own YOLO mode override, letting you control autonomy per-voice rather than globally
- Sessions now track their source (e.g. polyphon, poly CLI, Obsidian) and the sessions page has a filter dropdown to view sessions by source
- The TCP API now exposes an OpenRPC 1.3 machine-readable spec via `api.getSpec`, accessible without authentication — useful for IDE integrations and tooling
- The TCP API now includes a `settings.getUserProfile` endpoint
- The API Settings page shows a spec discovery info block with the `api.getSpec` endpoint URL

**Fixed**
- YOLO flags are now injected in the correct position for each CLI voice provider

[Download the latest release](https://polyphon.ai/#download)
