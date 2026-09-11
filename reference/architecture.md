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
         │   Modes: Manual · MCP · Copilot│
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

## Editor modes

Glint Web exposes the **same canvas verbs** three ways:

| Mode | Driver | Visibility |
|------|--------|------------|
| **Manual** | Human UI | Full editor |
| **Headless / MCP** | Agent tools / CI | Final assets only |
| **Copilot** | Agent + human | Live telepresence in the editor |

Design and phases: **[Editor modes](editor-modes.md)**. Copilot UX: **[Copilot mode](../guides/copilot-mode.md)**.

Agents use **Glint MCP** for Mode 2; Mode 3 adds a paired live session on top of those verbs (Canvas Agent API + telepresence).

## Data Flow

1. **Capture** - Capture package or Bridge produces ordered PNGs + `session.json`
2. **Design** - Web imports session, loads a template pack onto the frames board, exports ZIP (any mode)
3. **Preview** - View pastes session JSON with `data:` or `http(s)` screens (QR = metadata only)

## Roles

| Product | Owns |
|---------|------|
| Capture / Bridge | Real screenshots |
| Web | Templates, frames, export, editor modes |
| MCP | Agent tool surface for Capture / Bridge / headless export |
| View | On-device store listing preview |
