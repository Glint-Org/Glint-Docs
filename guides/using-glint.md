# How to use Glint

Glint turns **real app screens** into store-ready frames. Soft-launch path: **Capture/Bridge → Web → View**.

You can work **manually**, **with automation**, or **with an AI agent**. Same files: `session.json` + PNGs → Glint Web → ZIP → optional View preview.

## Manual

1. Capture
   - Flutter manual: `glint init` → edit rules → `glint capture`
   - Flutter auto: `glint capture --auto` (scans `lib/` for screens)
   - Or ask Cursor / Copilot to capture store screenshots
   - Or Android/web: Glint Bridge
   - Or drop PNG files into Glint Web
2. Open **Glint Web** (`cd Glint-Web && npm run dev`)
3. **Assets** → import the capture folder, or upload PNGs
4. **Templates** → pick a pack (loads frames onto the board)
5. **Frames** → headlines, colors, device screenshots, layer order
6. **Export** → Preview → ZIP; then **Copy for Glint View** for on-device QA

No account. Work stays on your machine.

## Automation

**Today**

- Add Capture as a Flutter `dev_dependency`
- Keep rules in `test/glint_screenshots_test.dart` (real widgets only)
- Run `glint capture` locally or in CI, or the repo scripts under `Glint-Capture/scripts/`
- Artifact: output folder with PNGs + `session.json`
- Import into Web and export the ZIP

**Roadmap:** headless Web / CLI polish so CI can emit the ZIP without a browser.

## AI agents

Follow:

- Skill: [glint-screenshot-workflow](../../Glint-Web/.cursor/skills/glint-screenshot-workflow/SKILL.md)
- Rule: [glint-ecosystem](../../Glint-Web/.cursor/rules/glint-ecosystem.mdc)
- Guide: [AI workflow](ai-workflow.md)

Typical loop: install Capture → real-screen rules → capture → import Web → template pack → export ZIP.

Agents **must not** generate fake UI.

## Docs

- [Setup](setup.md)
- [Workflow](workflow.md)
- [AI workflow](ai-workflow.md)
- [Session schema](../reference/session-schema.md)
- [Export spec](../reference/export-spec.md)
- [WebSocket protocol](../reference/websocket-protocol.md)
