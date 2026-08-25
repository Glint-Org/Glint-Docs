# Soft-launch smoke checklist

Run before every public soft-launch build. Mark each item.

## Capture

- [ ] `dart pub global activate --source path .` from Glint-Capture succeeds
- [ ] `glint init` in a Flutter app writes `glint.yaml` + test stub
- [ ] `glint capture` with soft-launch device `pixel9` only produces PNGs + `session.json`
- [ ] `session.json` has `version`, `app`, `screens`, and paths that resolve

## Bridge

- [ ] `python glint.py check` / `devices` lists ADB targets
- [ ] `python glint.py capture` writes PNG + session
- [ ] `python glint.py start` binds `ws://127.0.0.1:7700` with pairing token
- [ ] Glint Web → Capture from Device receives a frame

## Web

- [ ] `npm run build` succeeds; `npm run preview` serves the build
- [ ] Import Capture/Bridge folder → screenshots map onto frames
- [ ] Template swap replaces designs; screenshots stay
- [ ] Device → None strips bezels; Design chrome (radius / border / shadow) applies without freezing
- [ ] Device bezel re-select does **not** drift position
- [ ] Export ZIP unzip: Play `1080×1920`, iOS `1290×2796`, iPad `2048×2732` as selected
- [ ] Fastlane layout ZIP (when enabled) nests under `phoneScreenshots/` (or locale folder)
- [ ] Copy for Glint View pastes a session JSON View can open

## View

- [ ] Paste session → listing preview shows frames at store aspect

## Docs / hosting

- [ ] Hosted Web URL loads (Cloudflare / Vercel / GH Pages)
- [ ] Hosted Docs index links to Quick start + smoke checklist
- [ ] Golden path README steps complete in &lt; 15 minutes on a clean machine

## Agent path

- [ ] Skill / MCP: `glint_validate_session` accepts a Capture folder
- [ ] Skill / MCP: headless export produces a ZIP from session + template id
