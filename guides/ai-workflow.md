# AI-Assisted Glint Workflow

Developers can use Glint by hand, in CI, or with Cursor / Copilot / any agentic IDE. Rules and skills in this repo tell the agent what to do. The agent installs Capture, captures **real** UI, then uses Glint Web (with the same templates) to polish and export.

**Reference:** all of [Glint-Docs](../README.md) is markdown - read it here or on GitHub.

## What AI can do today

| Step | AI action | Tool |
|------|-----------|------|
| Install Capture | Add dependency, run `glint init` | Glint-Capture CLI |
| Define screens | Write `GLINTRule.screen()` rules | Dart test file |
| Capture | Run `glint capture` | Flutter test runner |
| Verify output | Check `session.json` + PNGs exist | Filesystem |
| Guide design | Pick template, write captions, recolor | Glint Web |
| Export | `{AppName}.zip` or `glint.zip` | Glint Web |

## What AI should not do

- Generate fake UI screenshots (App Store rejection risk)
- Skip real app widgets in Capture rules
- Mix Play and App Store sizes in one export batch
- Add misleading marketing copy

## Setup for Cursor

Project includes:

- **Skill:** `.cursor/skills/glint-screenshot-workflow/SKILL.md` - full pipeline instructions
- **Rule:** `.cursor/rules/glint-ecosystem.mdc` - always-on conventions

Ask your agent: *"Set up Glint Capture and capture store screenshots for this app"* - it should follow the skill.

## Example conversation

**Developer:** "I need Play Store screenshots for my Flutter app"

**AI should:**
1. Add `glint_capture` to dev_dependencies
2. Run `glint init`
3. Create rules for home, features, settings screens
4. Run `glint capture`
5. Instruct developer to open Glint Web → import `glint_screenshots/` folder
6. Recommend a graphic template (`play-hero`, `play-pop`, `ios-clean`)
7. Recolor art to brand colors, set tagline, export ZIP at 1080×1920

## Phase 2 (future)

- Glint SDK / headless Web export API for full agent automation
- Template selection via config file
- CI GitHub Action: capture → export → artifact upload

## Related docs

- [Setup](setup.md)
- [Workflow](workflow.md)
- [Session Schema](../reference/session-schema.md)
- [Export Spec](../reference/export-spec.md)
