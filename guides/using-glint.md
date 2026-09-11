# How to use Glint

Glint turns **real app screens** into store-ready frames. Soft-launch path: **Capture/Bridge → Web → View**.

You work in one of **three editor modes** — same verbs (import, template, bezel, scale, rotate, theme, export), different surfaces. Full design: [Editor modes](../reference/editor-modes.md).

| Mode | Who drives | What you see |
|------|------------|--------------|
| **1. Manual** | You in Glint Web | Full editor |
| **2. Headless / MCP** | Agent or CI via tools | Final screenshots / ZIP |
| **3. Copilot** | You + agent on one board | Agent actions live in the editor *(designed — see [Copilot](copilot-mode.md))* |

Same files throughout: `session.json` + PNGs → Glint Web → ZIP → optional View preview.

## Mode 1 — Manual

1. Capture
   - Flutter manual: `glint init` → edit rules → `glint capture`
   - Flutter auto: `glint capture --auto` (scans `lib/` for screens)
   - Or ask Cursor / Copilot to capture store screenshots (Mode 2 tools)
   - Or Android/web: Glint Bridge
   - Or drop PNG files into Glint Web
2. Open **Glint Web** (`cd Glint-Web && npm run dev`)
3. **Assets** → import the capture folder, or upload PNGs
4. **Templates** → pick a pack (loads frames onto the board)
5. **Frames** → headlines, colors, device screenshots, scale %, rotation °, layer order
6. **Export** → Preview → ZIP; then **Copy for Glint View** for on-device QA

No account. Work stays on your machine.

## Mode 2 — Headless / MCP (automation + agents)

**Today**

- Add Capture as a Flutter `dev_dependency`
- Keep rules in `test/glint_screenshots_test.dart` (real widgets only)
- Run `glint capture` locally or in CI, or the repo scripts under `Glint-Capture/scripts/`
- Or drive Capture / Bridge / export via **[Glint MCP](../../Glint-MCP/README.md)** from Cursor / Claude Code
- Artifact: output folder with PNGs + `session.json` (and optionally a ZIP from `glint_export`)
- Open Web only when you want Mode 1 polish

Agents **must not** generate fake UI. Details: [AI workflow](ai-workflow.md).

## Mode 3 — Copilot (watch + edit)

Designed path: agent drives the **same** editor controls you use, you watch (and can take over), then teach (“I fixed frame 1 — do the rest like this”).

- Guide: [Copilot mode](copilot-mode.md)
- Spec: [Editor modes](../reference/editor-modes.md)

Until Copilot ships, use Mode 2 for speed and Mode 1 for taste.

## Docs

- [Editor modes](../reference/editor-modes.md)
- [Copilot mode](copilot-mode.md)
- [Setup](setup.md)
- [Workflow](workflow.md)
- [AI workflow](ai-workflow.md)
- [Session schema](../reference/session-schema.md)
- [Export spec](../reference/export-spec.md)
- [WebSocket protocol](../reference/websocket-protocol.md)
