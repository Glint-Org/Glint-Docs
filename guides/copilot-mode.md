# Copilot mode (AI + developer)

**Mode 3** of Glint’s [editor modes](../reference/editor-modes.md): an agent and a human share the **Glint Web** frames board. The agent runs the same actions as the sidebar; the human can watch, pause, edit, and teach.

> **Status:** Designed. Manual (Mode 1) and Headless/MCP (Mode 2) are available today. Copilot builds on those — do not wait for Copilot to ship store screenshots; use Mode 1 + 2 now.

## When to use Copilot

- You want to **see** the agent select frames, move scale/rotation, swap bezels, extract theme.
- You will **interrupt** mid-run (“stop — use this headline instead”).
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
- Every visible move should map to a **verb** (scale %, angle °, bezel id, theme extract, …) — same as Mode 1 controls and Mode 2 tools.
- Watching is optional pacing (`present: true`); the underlying apply is identical to a silent tool call.

## Developer loop (target UX)

1. Open Glint Web with your session / pack loaded (Mode 1).
2. Start a **Copilot session** (pair token / “Allow agent” in the editor — local only).
3. In Cursor / Claude / Copilot, ask for changes in product language:
   - “On Frame 2, set device scale to 85% and rotation to −12°.”
   - “Extract theme from screenshots and apply.”
   - “Match Frames 3–5 to Frame 1’s bezel and scale.”
4. Watch the board update. Hit **Pause** or edit directly anytime.
5. After a manual fix: “I’ve adjusted Frame 1 — apply the same device transform to the rest.”
6. Export ZIP / Copy for Glint View as usual.

## Agent rules (Mode 3)

1. Call **canvas verbs** (or MCP editor tools) — do not invent pixels or fake UI screenshots.
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
| Edits headline copy | Copy style/structure only if asked — don’t overwrite other copy blindly |
| Extracts theme once | Reuse palette; don’t re-extract unless asked |

Reference selection explicitly in chat when possible: “use the **selected** device as the template.”

## Fallback today (until Copilot ships)

| You want | Do this now |
|----------|-------------|
| Fast agent output | Mode 2: MCP `glint_capture` → `glint_validate_session` → `glint_render` / `glint_export` |
| Visual polish | Mode 1: open Web, edit scale/rotation/theme (sidebar), export |
| “Watch something work” | Run Mode 2 in the IDE while Web is open for **after** review; or screen-share Mode 1 while you drive |

See [AI workflow](ai-workflow.md) and [Glint-MCP](../../Glint-MCP/README.md).

## Build checklist (for implementers)

Track against [editor-modes](../reference/editor-modes.md) phases:

- [ ] **P1** Canvas Agent API over existing helpers (`setDeviceUniformScale`, `setDeviceAngle`, `replaceDeviceFrame`, theme extract, …)
- [ ] **P2** MCP `glint_editor_*` (or live attach) against a paired editor tab
- [ ] **P3** Telepresence: cursor/focus, status line, Pause / Take over
- [ ] **P4** `matchFrame` / teach-from-selection helpers
- [ ] Docs + skill/rule updates when each phase lands
- [ ] Smoke: agent rotates device → human nudges ° → agent continues without clobbering

## Related

- [Editor modes](../reference/editor-modes.md)
- [Using Glint](using-glint.md)
- [AI workflow](ai-workflow.md)
- [Architecture](../reference/architecture.md)
- [Smoke checklist](smoke-checklist.md)
