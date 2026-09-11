# Glint Docs

Public reference for the Glint ecosystem. **These markdown files are the docs** - read them in the repo or on GitHub.

Soft-launch path: **Capture / Bridge → Web (frames) → View (preview)**.

## Start here

- [**Golden path**](guides/golden-path.md) - first ZIP in &lt; 15 minutes
- [Smoke checklist](guides/smoke-checklist.md) - pre-release QA
- [How to use Glint](guides/using-glint.md) - Manual · Headless/MCP · Copilot
- [Editor modes](reference/editor-modes.md) - three ways to drive the same verbs
- [Copilot mode](guides/copilot-mode.md) - watch AI work + teach-by-edit *(design)*
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
| **Glint-MCP** | Agent tools for Capture / Bridge / headless export |
| **Glint-View** | Store Room + listing preview; `.glint` round-trip |

## Reference

- [Architecture](reference/architecture.md)
- [Editor modes](reference/editor-modes.md)
- [Session schema](reference/session-schema.md)
- [Project pack (.glint)](reference/project-pack.md)
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

---

<div align="center">

<a href="https://github.com/darkmintis">
  <img src="https://img.shields.io/badge/follow-%40Darkmintis-1DA1F2?style=social&logo=github" alt="Follow @Darkmintis"/>
</a>

</div>
