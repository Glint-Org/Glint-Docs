# Telor Docs

Reference documentation for the Telor screenshot automation ecosystem.

## Repos

| Repo | Purpose |
|------|---------|
| **Telor-Capture** | Flutter package — device-free golden screenshot capture |
| **Telor-Bridge** | Python ADB capture engine for Android devices |
| **Telor-Web** | React editor with viral templates and batch export |
| **Telor-View** | Flutter Play/App Store preview app |

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
telor_capture → session.json + PNGs → Telor Web templates → ZIP export → Telor View QR
```

Or for non-Flutter apps:

```
Telor Bridge (ADB) → output/session.json → Telor Web → Telor View
```
