# How to use Glint

Glint is built to be **simple to use** and **stable enough for shipping store assets**. Capture real screens, polish them in the editor, export at official store sizes.

You can work **manually**, **with automation**, or **with an AI agent**. All three use the same files: `session.json` + PNGs → Glint Web → ZIP.

## Manual

Best when you already have screenshots or want full control in the editor.

1. Capture
   - Flutter: `glint init` then `glint capture` (see [Setup](setup.md))
   - Or Android device: Glint Bridge
   - Or drop PNG files into Glint Web
2. Open **Glint Web** (`cd Glint-Web && npm run dev`)
3. **Assets** → import the capture folder, or upload PNGs
4. **Templates** → pick one graphic layout and keep it for the whole set
5. **Design** → headlines, colors, device frame or rounded screenshot, graphics
6. **Export** → Play / App Store / iPad ZIP

No account. Work stays on your machine.

## Automation

Best when screenshots should stay in sync with the app.

**Today**

- Check Capture into the Flutter app as a dev dependency
- Keep rules in `test/glint_screenshots_test.dart` (real widgets only)
- Run `glint capture` locally or in CI, or the repo scripts:

```bash
chmod +x /path/to/Glint-Org/Glint-Capture/scripts/*.sh
cd /path/to/your_flutter_app
/path/to/Glint-Org/Glint-Capture/scripts/glint-init.sh
/path/to/Glint-Org/Glint-Capture/scripts/glint-capture.sh
```
- Artifact: output folder with PNGs + `session.json`
- A person (or agent) imports that folder into Web and exports the ZIP

**Next (roadmap)**

- Headless Web / CLI export so CI can emit the polished ZIP without opening a browser
- GitHub Action: capture → polish → upload artifact

Until that lands, automation covers **capture**; polish still goes through Glint Web.

## AI agents

Best when you do not want to spend time on capture setup or first-pass design.

Agents in Cursor, Copilot, or any agentic IDE should follow:

- Skill: [glint-screenshot-workflow](../../Glint-Web/.cursor/skills/glint-screenshot-workflow/SKILL.md)
- Rule: [glint-ecosystem](../../Glint-Web/.cursor/rules/glint-ecosystem.mdc)
- Guide: [AI workflow](ai-workflow.md)

Typical agent loop:

1. Install `glint_capture`, run `glint init`
2. Write `GLINTRule.screen()` for **real** app screens
3. Run `glint capture`, confirm `session.json` + PNGs
4. Open / import into Glint Web, apply a graphic template, match brand colors
5. Export ZIP at the correct store size

Agents **must not** generate fake UI. Apple and Google reject listings that do not show the shipped app.

## Docs

[Glint-Docs](../README.md) is the reference. Read it in the repo or on GitHub - every guide and schema is a markdown file.

- [Setup](setup.md)
- [Workflow](workflow.md)
- [AI workflow](ai-workflow.md)
- [Session schema](../reference/session-schema.md)
- [Export spec](../reference/export-spec.md)
