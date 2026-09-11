# Copilot mode (AI + developer)

**Mode 3** of Glint’s [editor modes](../reference/editor-modes.md): an agent and a human share the **Glint Web** frames board. The agent runs the same actions as the sidebar; the human can watch, pause, edit, and teach.

> **Status:** Scaffold live in Glint Web. Open the editor → **Allow agent** on the Copilot bar → **Demo** to watch a presented rotate, or drive `window.__GLINT_COPILOT__` from the console. MCP `glint_editor_*` attach is next. Mode 1 + Mode 2 remain the production paths for shipping ZIPs.

## When to use Copilot

- You want to **see** the agent select frames, move scale/rotation, swap bezels, extract theme.
- You will **interrupt** mid-run (“stop - use this headline instead”).
- You fixed one frame by hand and want: **“do the other frames like this.”**

Use **Headless / MCP** instead when you only care about the ZIP and speed (CI, overnight packs).

Use **Manual** when taste matters more than automation.

## Mental model

```
You (chat)  →  Agent  →  Canvas verbs  →  Live editor
                              ↑                │
                              └── your edits ──┘
```

- **Truth** lives in the open project (canvas + `.glint` / session), not in the chat.
- Every visible move should map to a **verb** (scale %, angle °, bezel id, theme extract, …) - same as Mode 1 controls and Mode 2 tools.
- Watching is optional pacing (`present: true`); the underlying apply is identical to a silent tool call.

## Developer loop (target UX)

1. Open Glint Web with your session / pack loaded (Mode 1).
2. Click **Allow agent** on the Copilot bar (shows pair token + unlocks `window.__GLINT_COPILOT__`).
3. Drive changes:
   - **Demo** on the bar (presented select → rotate), or
   - From DevTools / a local agent: `await __GLINT_COPILOT__.dispatch('setDeviceScale', { frameIndex: 0, pct: 85 }, { present: true, expectedGeneration: (await __GLINT_COPILOT__.getEditorState()).generation, token: __GLINT_COPILOT__.getToken() })`
   - Chat agents (once MCP attach ships): “On Frame 2, set device scale to 85% and rotation to −12°.”
4. Watch the board update (status line + frame pulse). Hit **Pause** or edit directly anytime.
5. After a manual fix: ask to match other frames (API: `matchDeviceTransform`), or re-Allow and continue from a fresh `getEditorState`.
6. Export ZIP / Copy for Glint View as usual.

## Agent rules (Mode 3)

1. Call **canvas verbs** (or MCP editor tools) - do not invent pixels or fake UI screenshots.
2. Before a multi-frame batch, call **`getEditorState`** (or equivalent) so human edits win.
3. Prefer small, narrated steps when `present: true` (select frame → select device → set value).
4. On **Pause / Take over**, stop issuing verbs until the human resumes.
5. Never ask for Capture LLM API keys for Glint polish; Capture/Bridge remain real-screen only.
6. Soft-launch device defaults stay in force (e.g. Capture **pixel9** unless the project says otherwise).

## Teach-from-edit

Human polish is the best prompt.

| Human action | What the agent should do |
|--------------|--------------------------|
| Selects Frame #1 device, sets scale 90%, angle −6° | Read transform; apply to other frames if asked |
| Changes bezel on one slide | Propagate bezel id when asked to “match” |
| Edits headline copy | Copy style/structure only if asked - don’t overwrite other copy blindly |
| Extracts theme once | Reuse palette; don’t re-extract unless asked |

Reference selection explicitly in chat when possible: “use the **selected** device as the template.”

## Fallback / hybrid today

| You want | Do this |
|----------|---------|
| Fast agent output | Mode 2: MCP `glint_capture` → validate → `glint_render` / `glint_export` |
| Visual polish | Mode 1: open Web, edit scale/rotation/theme, export |
| Watch AI on the board | Mode 3: **Allow agent** → **Demo**, or `window.__GLINT_COPILOT__.dispatch(...)` |

See [AI workflow](ai-workflow.md) and [Glint-MCP](../../Glint-MCP/README.md).

## Build checklist (for implementers)

Track against [editor-modes](../reference/editor-modes.md) phases:

- [x] **P1** Canvas Agent API over existing helpers (`setDeviceUniformScale`, `setDeviceAngle`, …)
- [x] **P2a** In-editor Copilot session + generation + `window.__GLINT_COPILOT__`
- [ ] **P2b** MCP `glint_editor_*` against a paired editor tab
- [x] **P3a** Telepresence: status line, Pause / Take over, frame pulse
- [ ] **P3b** Branded agent cursor path to controls
- [x] **P4a** `matchDeviceTransform` helper
- [ ] **P4b** “Match other frames” UI + bezel/theme verbs in session
- [ ] Smoke: agent rotates device → human nudges ° → agent continues without clobbering

## Related

- [Editor modes](../reference/editor-modes.md)
- [Using Glint](using-glint.md)
- [AI workflow](ai-workflow.md)
- [Architecture](../reference/architecture.md)
- [Smoke checklist](smoke-checklist.md)
