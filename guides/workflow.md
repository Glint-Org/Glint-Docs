# Development Workflow

## Full Pipeline (End to End)

### Path A: Glint Capture (Flutter, no device)

```
Flutter app + screenshot rules → glint capture → glint_screenshots/ (+ session.json)
```

1. Add `glint_capture` to `dev_dependencies`
2. Run `glint init` (or create `test/glint_screenshots_test.dart` with `glintScreenshots()` rules)
3. Edit `glint.yaml` - app name, tagline, store, devices
4. Run: `glint capture` (or `flutter test test/glint_screenshots_test.dart`)
5. Output: PNGs under `android|ios/<device>/` **and** root `session.json`

### Path B: Glint Bridge (Android device)

```
Android Device → USB/WiFi → Glint Bridge → output/ + session.json
```

- Connect device via USB debugging or WiFi ADB
- Run Bridge in server mode (`python glint.py start`) or use `capture` / `batch` / `crawl`
- Output goes to `Glint-Bridge/output/` with auto-generated `session.json`
- Server is localhost-only and requires a pairing token before Web can connect

### Step 2: Design (Glint Web)

```
session.json + PNGs → Glint Web → curated template → batch PNG/ZIP export
```

- Import session folder (drag Capture output or Bridge `output/`)
- Pick a graphic Play / App Store / iPad template (blobs, waves, rings - editable)
- Edit on the canvas: recolor graphics, rewrite headlines, adjust device frames
- Export batch ZIP (Play Store 1080×1920 or App Store 1290×2796 / iPad 2048×2732)

### Step 3: Preview (Glint View)

```
session.json → QR code → Glint View → Play/App Store preview
```

- Export session generates JSON with screenshot filenames
- View on device by scanning QR or pasting JSON
- Swipe through carousel like real store listing
- Validate design before publishing

## Development Tips

- **Glint-Capture:** Prefer `glint capture`; the runner writes `session.json` in `tearDownAll`, and the CLI refreshes it after the test run
- **Bridge:** Test with `python glint.py devices` first; use `python glint.py start` for live Web pairing
- **Web:** Hot module reload works - templates and frames update instantly
- **View:** Use `flutter run --debug` for quick iteration on preview layout
- **Cross-repo:** Keep Bridge WebSocket running while developing Web features; always pair with the token

## Adding Features

| Area | Typical Change |
|------|---------------|
| New template | Add JSON to `Glint-Web/public/templates/` and register in `templateLoader.js` |
| New device preset | Add to `Glint-Capture/lib/src/devices.dart` |
| New export format | Extend `exportHelper.js` EXPORT_PRESETS |
| New frame SVG | Add SVG to `public/frames/` + insets in `frameMeta.js` |
| New preview layout | Add widget in `Glint-View/lib/widgets/` |
| Bridge action | Add handler in `websocket_server.py` + client method in `useGlintBridge.js` |
