# AI-assisted workflow

Use Glint by hand (**Mode 1**), ask **Cursor / Claude / Copilot** to run tools (**Mode 2**), or share a live editor session (**Mode 3** Copilot). The agent is the brain - you should not paste Capture LLM API keys into Glint for polish.

**Modes:** [Editor modes](../reference/editor-modes.md) · **Copilot:** [Copilot mode](copilot-mode.md)

## Dual capture → Web polish

```
┌─ Capture (Flutter, no device) ─┐
│  Manual: write GLINTRules      │
│  Auto: glint capture --auto    │──► session.json + PNGs ──► Glint Web
│  Agent: discover + capture     │         │                    (templates,
└────────────────────────────────┘         │                     polish, ZIP)
┌─ Bridge (device / web) ────────┐         │
│  Manual: capture / batch       │─────────┘
│  Crawl: heuristic or --ai      │
└────────────────────────────────┘
```

| Path | Manual (Mode 1) | Headless / agent (Mode 2) |
|------|-----------------|---------------------------|
| Capture | Edit rules → `glint capture` | `glint capture --auto` or MCP `glint_capture` |
| Bridge | `capture` / `batch` | crawl / MCP Bridge tools |
| Design | Glint Web sidebar | `glint_render` / export tools |
| Live co-edit | - | Mode 3 Copilot |

## What the agent should do (Mode 2)

| Step | Action | Tool |
|------|--------|------|
| Discover Flutter screens | Scan `lib/`, write real `GLINTRule`s | `glint discover` / MCP `glint_discover` |
| Capture Flutter | Widget-test screenshots | `glint capture` / MCP `glint_capture` |
| Crawl Android/web | Real device/browser frames | Bridge / MCP Bridge tools |
| Validate | Check session + PNGs | MCP `glint_validate_session` |
| Compose / edit | Headlines, colors, bezel (no browser) | MCP `glint_render` |
| Polish by eye | Templates, captions, scale, rotation | Glint Web (Mode 1) |
| Export | ZIP | Web or `glint_export` |
| Live “watch me work” | Shared board + telepresence | Mode 3 - see [Copilot](copilot-mode.md) |

## What AI should not do

- Ask developers for OpenAI/Anthropic keys for **Capture**
- Generate fake UI screenshots
- Leave placeholder scaffolds when real screens exist
- Clobber human canvas edits without re-reading editor state (especially in Mode 3)

## Example

**Developer:** "Capture Play Store screenshots for this Flutter app"

**Agent should:** `glint init` if needed → discover/write real rules → `glint capture` → validate → either `glint_export` / `glint_render` (Mode 2) or point them at Glint Web for Mode 1 polish.

**Developer (later):** "I'm in the editor - match the other frames to my Frame 1 device size and angle"

**Agent should (Mode 3):** read editor state → apply canvas verbs with telepresence → stop if they Pause / Take over.

## Related docs

- [Editor modes](../reference/editor-modes.md) · [Copilot mode](copilot-mode.md)
- [Setup](setup.md) · [Workflow](workflow.md) · [Using Glint](using-glint.md)
- [Glint-MCP](https://github.com/Glint-Org/Glint-MCP)
