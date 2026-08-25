# Architecture

```
         ┌──────────────────────────────┐
         │   GLINT CAPTURE               │
         │   Flutter package + CLI       │
         │   Widget-test screenshots     │
         └────────────┬─────────────────┘
                      │ session.json + PNGs
                      ▼
         ┌──────────────────────────────┐
         │   GLINT BRIDGE                │
         │   ADB (+ optional Appium)     │
         │   CLI + ws://127.0.0.1:7700   │
         │   pairing token + data_urls   │
         └────────────┬─────────────────┘
                      │
                      ▼
         ┌──────────────────────────────┐
         │   GLINT WEB                   │
         │   React + Vite + Fabric.js   │
         │   Frames board + templates   │
         │   ZIP export + View clipboard │
         └────────────┬─────────────────┘
                      │ paste session (data: screens)
                      ▼
         ┌──────────────────────────────┐
         │   GLINT VIEW                  │
         │   Flutter store listing QA    │
         │   Preview only (no editor)    │
         └──────────────────────────────┘
```

## Capture Paths

| Path | Tool | Requires Device |
|------|------|-----------------|
| Code-based | `glint_capture` Flutter package | No |
| Device-based | Glint Bridge (ADB) | Yes (Android) |
| Manual | Upload to Glint Web | No |

## Data Flow

1. **Capture** - Capture package or Bridge produces ordered PNGs + `session.json`
2. **Design** - Web imports session, loads a template pack onto the frames board, exports ZIP
3. **Preview** - View pastes session JSON with `data:` or `http(s)` screens (QR = metadata only)

## Roles

| Product | Owns |
|---------|------|
| Capture / Bridge | Real screenshots |
| Web | Templates, frames, export |
| View | On-device store listing preview |
