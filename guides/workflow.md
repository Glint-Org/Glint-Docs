# Development Workflow

## Full Pipeline (End to End)

### Path A: telor_capture (Flutter, no device)

```
Flutter app + screenshot rules → telor_capture CLI → build/telor_screenshots/
```

1. Add `telor_capture` to dev_dependencies
2. Create `test/telor_screenshots_test.dart` with `telorScreenshots()` rules
3. Run: `dart run telor_capture --app MyApp --output build/telor_screenshots`
4. Output: PNGs + `session.json`

### Path B: Telor Bridge (Android device)

```
Android Device → USB/WiFi → Telor Bridge → output/ + session.json
```

- Connect device via USB debugging or WiFi ADB
- Run Bridge in server mode or use `capture`/`batch`/`crawl` CLI commands
- Output goes to `Telor-Bridge/output/` with auto-generated `session.json`

### Step 2: Design (Telor Web)

```
session.json + PNGs → Telor Web → viral template → batch PNG/ZIP export
```

- Import session folder (drag `build/telor_screenshots/` or Bridge `output/`)
- Pick a viral template from the gallery
- All screenshots auto-composed with device frames and backgrounds
- Export batch ZIP (Play Store 1080×1920 or App Store 1290×2796)

### Step 3: Preview (Telor View)

```
session.json → QR code → Telor View → Play/App Store preview
```

- Export session generates JSON with screenshot URLs
- View on device by scanning QR or pasting JSON
- Swipe through carousel like real store listing
- Validate design before publishing

## Development Tips

- **Telor-Capture:** Run `flutter test test/telor_screenshots_test.dart --update-goldens` for quick iteration
- **Bridge:** Test with `python -m bridge.main devices` to verify ADB connection first
- **Web:** Hot module reload works — templates and frames update instantly
- **View:** Use `flutter run --debug` for quick iteration on preview layout
- **Cross-repo:** Keep Bridge WebSocket running while developing Web features

## Adding Features

| Area | Typical Change |
|------|---------------|
| New template | Add JSON to `Telor-Web/public/templates/` and register in `templateLoader.js` |
| New device preset | Add to `Telor-Capture/lib/src/devices.dart` |
| New export format | Extend `exportHelper.js` EXPORT_PRESETS |
| New frame SVG | Add SVG to `public/frames/` and update `FrameSelector.jsx` |
| New preview layout | Add widget in `Telor-View/lib/widgets/` |
| Bridge action | Add handler in `websocket_server.py` + client method in `useTelorBridge.js` |
