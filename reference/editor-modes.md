# Editor modes (Manual · Headless · Copilot)

Glint has **one set of verbs** (import shots, pick template, set bezel, scale, rotate, theme, export). Those verbs are exposed three ways so humans and agents share the same outcome without three different products.

| Mode | Who drives | What the user sees | Best for |
|------|------------|--------------------|----------|
| **1. Manual** | Human in Glint Web | Full editor | Polish, taste, last-mile edits |
| **2. Headless / MCP** | Agent or CI via tools | Final screenshots / ZIP (no live show) | Speed, CI, overnight packs |
| **3. Copilot** | Agent + human on one board | Agent actions play out in the editor | Demos, trust, “watch AI work”, teach-by-edit |

```
                    ┌─────────────────────────┐
                    │   Shared canvas verbs    │
                    │  select · scale · angle  │
                    │  bezel · theme · export  │
                    └────────────┬────────────┘
           ┌─────────────────────┼─────────────────────┐
           ▼                     ▼                     ▼
     ┌───────────┐        ┌─────────────┐       ┌──────────────┐
     │  Manual   │        │ Headless /  │       │   Copilot    │
     │  (UI)     │        │ MCP         │       │  UI + agent  │
     └───────────┘        └─────────────┘       └──────────────┘
```

## Mode 1 — Manual

**Status:** shipped.

Open Glint Web, import a session or PNGs, pick a template pack, edit frames on the board (device bezel, scale %, rotation °, colors, headlines), export ZIP / hand off to View.

- No agent required.
- Source of truth while editing: live Fabric canvas + project pack (`.glint`).
- Docs: [Using Glint](../guides/using-glint.md), [Workflow](../guides/workflow.md).

## Mode 2 — Headless / MCP

**Status:** shipped (Capture / Bridge / validate / render / export tools).

An IDE agent (Cursor, Claude Code, Copilot) or CI calls **MCP / CLI** tools. Work happens **offstage** — no fake cursor in the editor. The user reviews **outputs** (session folder, rendered PNGs, ZIP).

| Concern | How Mode 2 handles it |
|---------|------------------------|
| Capture | `glint_discover` / `glint_capture` / Bridge tools |
| Validate | `glint_validate_session` |
| Compose / edit without browser | `glint_render` (and related tools) |
| Store ZIP | `glint_export` against Web `/export` |

Rules:

- Prefer **real** app screens — never fabricate UI tiles (App Store 2.3.10).
- Agent is the intelligence; do not paste Capture LLM keys into the product for Mode 2 polish.
- Docs: [AI workflow](../guides/ai-workflow.md), [Glint-MCP README](../../Glint-MCP/README.md).

## Mode 3 — Copilot (AI + developer)

**Status:** designed — build in phases (see below). Manual + MCP already cover the verbs; Copilot adds a **live shared session** so those verbs are visible and interruptible.

### Goals

1. Developer tells the agent what to do in plain language (“darker frame 2, rotate −8°, extract theme”).
2. User **watches** the editor respond (selection, controls, optional cursor) — fun and trustworthy, like competitor “AI at work” demos.
3. User can **grab the wheel**: pause, nudge scale/rotation/copy by hand, then say “I fixed frame 1 — do the others like this.”
4. Same pack / session files Mode 1 and 2 already use — no parallel truth.

### Non-goals

- Replacing Mode 2 for CI (Copilot is slower by design).
- Driving the editor only via raw DOM Playwright long-term (fine for prototypes; MCP + telepresence is the product path).
- Generating fake screenshots.

### Architecture

```
  IDE agent (Cursor / Claude / …)
        │  intent (“make frames match frame 1”)
        ▼
  ┌─────────────────┐     tool calls      ┌──────────────────┐
  │  Glint MCP      │ ──────────────────► │  Canvas Agent    │
  │  (+ copilot     │                     │  API (verbs)     │
  │   session id)   │ ◄────────────────── │  in Glint Web    │
  └────────┬────────┘   ack + state       └────────┬─────────┘
           │                                         │
           │                              apply + emit events
           │                                         ▼
           │                              ┌──────────────────┐
           │                              │  Telepresence    │
           └──── optional live tail ─────►│  (cursor, focus, │
                                          │   status toast)  │
                                          └────────┬─────────┘
                                                   ▼
                                          Human sees + edits
```

**Shared verbs (Canvas Agent API)** — one implementation used by UI handlers and by agents:

| Verb | Example |
|------|---------|
| `selectFrame(i)` | Focus artboard / Frame #N |
| `selectDevice` | Active framed device |
| `setDeviceScale(pct)` | Same as sidebar Scale % |
| `setDeviceAngle(deg)` | Same as sidebar Rotation ° |
| `setDeviceBezel(frameId)` | FrameSelector |
| `setScreenshot(url)` | Import / replace / clear |
| `extractTheme` | Colors → Extract theme |
| `setHeadline(i, text)` | Text layers |
| `exportZip` / `savePack` | Export / `.glint` |

**Telepresence** — every verb emits a short event stream (`select` → `pointerMove` → `apply` → `done`). The UI:

- Moves a branded agent cursor (or selection pulse) to the target control / device.
- Updates the real canvas (not a video of another machine).
- Shows a small status line: “Agent: rotation −8° on Frame 2”.
- Honors **Pause / Take over** so the human can edit without racing the agent.

**Teach-from-edit** — after the human changes Frame 1:

1. Agent reads current pack / selection (`getEditorState`).
2. Diff or explicit “reference frame” id.
3. Replays verbs on Frames 2…N (Mode 2-speed under the hood, Mode 3 visuals if Copilot session is live).

### Protocol sketch

Local-only channel (WebSocket or same-origin EventSource) tied to an open editor tab:

```json
{
  "sessionId": "copilot-…",
  "op": "setDeviceAngle",
  "args": { "frameIndex": 1, "degrees": -8 },
  "present": true,
  "paceMs": 420
}
```

- `present: false` → apply immediately (Mode 2 behavior inside an open tab).
- `present: true` → telepresence pacing for demos.
- Human edits bump a `generation` counter; agent must re-`getEditorState` before the next batch (“I’ve changed this — continue from here”).

Auth: localhost + short-lived token (same idea as Bridge pairing) — never expose the canvas agent on a public URL without auth.

### Implementation phases

| Phase | Deliverable | Unlocks |
|-------|-------------|---------|
| **P0** | Document modes; keep Manual + MCP solid | Shared language for product/eng |
| **P1** | Canvas Agent API wrapping existing editor helpers (`setDeviceUniformScale`, `setDeviceAngle`, bezel swap, theme extract, …) | Agents call the same code paths as the sidebar |
| **P2** | MCP tools that hit a running Web editor (`glint_editor_*`) **or** extend `glint_render` with a live attach mode | Mode 3 without Playwright |
| **P3** | Telepresence layer (cursor, toasts, pause/takeover) | “Fun to watch” |
| **P4** | Teach-from-selection / “match frame N” | Competitor-style iterate loop |

Until P2–P3 ship, agents should use Mode 2 and invite humans into Mode 1 for polish — already documented in [AI workflow](../guides/ai-workflow.md).

### Mode choice cheat sheet

| Situation | Use |
|-----------|-----|
| Tweaking one headline by eye | **Manual** |
| CI nightly store ZIP | **Headless / MCP** |
| Demo for stakeholders / teaching the agent from a fixed frame | **Copilot** |
| Capture only, design later | Capture/Bridge → then any mode |

## Related

- [Copilot mode guide](../guides/copilot-mode.md) — how developers and agents should work in Mode 3
- [Architecture](architecture.md)
- [AI workflow](../guides/ai-workflow.md)
- [Using Glint](../guides/using-glint.md)
