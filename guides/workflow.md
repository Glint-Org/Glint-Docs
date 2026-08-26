# Development Workflow

## Full Pipeline (End to End)

### Path A: Glint Capture (Flutter, no device)

```
Flutter app + rules OR AI discover → glint capture → glint_screenshots/ (+ session.json)
```

1. Add `glint_capture` to `dev_dependencies` (path or git; see Capture README)
2. Run `glint init` (or create `test/glint_screenshots_test.dart` with `glintScreenshots()` rules)
3. Edit `glint.yaml` - app name, tagline, store, devices
4. **Manual:** edit rules with real widgets → `glint capture`  
   **Auto:** `glint capture --auto` (scans `lib/` `*Screen`/`*Page`, writes builders, captures)  
   **Agent:** ask Cursor / Copilot — no API keys
5. Output: PNGs under `android|ios/<device>/` **and** root `session.json` (primary device paths for Web frames)

**Tip:** Soft launch with one device (e.g. `pixel9`) so frames map 1:1 to your screen sequence.

### Path B: Glint Bridge (Android device)

```
Android Device → USB/WiFi → Glint Bridge → output/ + session.json
```

- Connect device via USB debugging or WiFi ADB
- Run Bridge in server mode (`python glint.py start`) or use `capture` / `batch` / `crawl`
- **Intelligent crawl:** `export GLINT_AI_API_KEY=...` then `python glint.py crawl com.app --ai` (or `crawl-web URL --ai`). AI navigates and keeps store-worthy **real** screens only; keys stay on your machine.
- Output goes to `Glint-Bridge/output/` with auto-generated `session.json`
- Server is localhost-only and requires a pairing token before Web can connect
- Live captures include `data_url` / `data_urls` so the browser can display PNGs

### Step 2: Design (Glint Web)

```
session.json + PNGs → Glint Web → template pack → frames board → ZIP
```

- Import session folder (drag Capture output or Bridge `output/`)
- Pick a **platform → device** template pack (loads 1–10 frames)
- Edit on the **frames board**: headlines, colors, device screenshots, layers
- Export ZIP (Play 1080×1920, App Store phone, or iPad sizes)

### Step 3: Preview (Glint View) — preview only

```
Web Export → Preview frames → Copy for Glint View → paste in View
```

- Prefer **Copy for Glint View** after Preview/Export (includes full `data:` screens)
- QR from Web carries **metadata only** (screenshots are too large for QR)
- View shows Play / App Store style listing chrome — no frame editor

## Development Tips

- **Glint-Capture:** Prefer `glint capture`; the runner writes `session.json` in `tearDownAll`
- **Bridge:** `python glint.py devices` first; `python glint.py start` for live Web pairing
- **Web:** Frames board (not an infinite canvas); templates live in `public/templates/`
- **View:** Paste Session JSON for image-backed preview; FVM Flutter 3.44.1
- **Cross-repo:** Keep Bridge WebSocket running while developing Web capture; always pair with the token

## Adding Features

| Area | Typical Change |
|------|---------------|
| New template pack | Add JSON to `Glint-Web/public/templates/` and register in `templateLoader.js` |
| New device preset | Add to `Glint-Capture/lib/src/devices.dart` |
| New export format | Extend `exportHelper.js` EXPORT_PRESETS |
| New frame SVG | Add SVG to `public/frames/` + insets in `frameMeta.js` |
| New preview layout | Add widget in `Glint-View/lib/widgets/` |
| Bridge action | Add handler in `websocket_server.py` + client method in `useGlintBridge.js` |
