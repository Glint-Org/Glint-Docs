# Glint Docs

Public reference for the Glint ecosystem. **These markdown files are the docs** - read them in the repo or on GitHub.

Soft-launch path: **Capture / Bridge → Web (frames) → View (preview)**.

## Start here

- [**Golden path**](guides/golden-path.md) - first ZIP in &lt; 15 minutes
- [Smoke checklist](guides/smoke-checklist.md) - pre-release QA
- [How to use Glint](guides/using-glint.md) - manual, automation, and AI
- [Setup](guides/setup.md) - install Capture, Bridge, Web, View
- [Workflow](guides/workflow.md) - capture → design → export → preview
- [AI workflow](guides/ai-workflow.md) - Cursor / Copilot / agents / MCP
- [Store upload](guides/store-upload.md) - Play / ASC / Fastlane

## Products

| Product | Purpose |
|---------|---------|
| **Glint-Capture** | Flutter package - device-free capture + `session.json` |
| **Glint-Bridge** | Python ADB capture for Android (+ localhost WebSocket) |
| **Glint-Web** | Frames editor - template packs, layers, ZIP, View handoff |
| **Glint-View** | On-device Play / App Store listing preview (no editor) |

## Reference

- [Architecture](reference/architecture.md)
- [Session schema](reference/session-schema.md)
- [Export spec](reference/export-spec.md)
- [WebSocket protocol](reference/websocket-protocol.md)
- [Frames](reference/frames.md)
- [Project structure](reference/project-structure.md)

## Pipeline

```
glint capture  →  session.json + PNGs  →  Glint Web  →  ZIP
                                          ↓ Copy for Glint View
                                       Glint View (paste)
```

Non-Flutter Android:

```
Glint Bridge  →  output/session.json (+ data_urls via WS)  →  Glint Web  →  View
```
