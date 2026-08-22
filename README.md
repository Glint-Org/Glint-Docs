# Glint Docs

Reference documentation for the Glint screenshot automation ecosystem.

## Repos

| Repo | Purpose |
|------|---------|
| **Glint-Capture** | Flutter package — device-free golden screenshot capture |
| **Glint-Bridge** | Python ADB capture engine for Android devices |
| **Glint-Web** | React editor with viral templates and batch export |
| **Glint-View** | Flutter Play/App Store preview app |

## Guides

- [Setup](guides/setup.md) — install all components
- [Workflow](guides/workflow.md) — end-to-end capture → design → preview

## Reference

- [Architecture](reference/architecture.md) — system overview and data flow
- [Session Schema](reference/session-schema.md) — JSON format for cross-tool handoff
- [Export Spec](reference/export-spec.md) — store dimension requirements
- [WebSocket Protocol](reference/websocket-protocol.md) — Bridge API
- [Frames](reference/frames.md) — device frame SVG guide
- [Project Structure](reference/project-structure.md) — repo layout

## Quick Workflow

```
glint_capture → session.json + PNGs → Glint Web templates → ZIP export → Glint View QR
```

Or for non-Flutter apps:

```
Glint Bridge (ADB) → output/session.json → Glint Web → Glint View
```
