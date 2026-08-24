# Glint Docs

Public reference for the Glint ecosystem. **These markdown files are the docs** - read them in the repo or on GitHub. No extra site required.

Glint is simple to use, stable for shipping store assets, and usable **by hand**, **in automation**, or **with an AI agent**.

## Start here

- [How to use Glint](guides/using-glint.md) - manual, automation, and AI
- [Setup](guides/setup.md) - install Capture, Bridge, Web, View
- [Workflow](guides/workflow.md) - capture → design → export → preview
- [AI workflow](guides/ai-workflow.md) - Cursor / Copilot / agents

## Products

| Product | Purpose |
|---------|---------|
| **Glint-Capture** | Flutter package - device-free capture + `session.json` |
| **Glint-Bridge** | Python ADB capture for Android |
| **Glint-Web** | Editor - graphic templates, canvas, ZIP export |
| **Glint-View** | On-device Play / App Store preview |

## Reference

- [Architecture](reference/architecture.md)
- [Session schema](reference/session-schema.md)
- [Export spec](reference/export-spec.md)
- [WebSocket protocol](reference/websocket-protocol.md)
- [Frames](reference/frames.md)
- [Project structure](reference/project-structure.md)

## Pipeline

```
glint capture  →  session.json + PNGs  →  Glint Web  →  ZIP  →  Glint View (optional)
```

Non-Flutter Android:

```
Glint Bridge  →  output/session.json  →  Glint Web  →  Glint View
```
