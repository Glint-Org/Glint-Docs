# Development Workflow

## Full Pipeline (End to End)

### Step 1: Capture
```
Android Device → USB/WiFi → Telor Bridge → screenshots + session.json
```

- Connect device via USB debugging or WiFi ADB
- Run Bridge in server mode or use `capture`/`batch` CLI commands
- Output goes to `Telor-Bridge/output/`

### Step 2: Design
```
screenshots → Telor Web → frame + theme + text → PNG export
```

- Upload screenshots or let Bridge auto-connect (WebSocket)
- Select device frame (if available)
- Choose background theme (solid / gradient / glass)
- Add text overlays (app name, tagline)
- Rearrange screenshots in desired order
- Export single frame or batch ZIP

### Step 3: Preview
```
session.json → QR code → Telor View → Play Store preview
```

- Export session generates JSON with screenshot URLs
- View on device by scanning QR or pasting JSON
- Swipe through carousel like real Play Store listing
- Validate design before publishing

## Development Tips

- **Bridge:** Test with `python -m bridge.main devices` to verify ADB connection first
- **Web:** Hot module reload works — themes and frames update instantly
- **View:** Use `flutter run --debug` for quick iteration on preview layout
- **Cross-repo:** Keep Bridge WebSocket running while developing Web features

## Adding Features

| Area | Typical Change |
|------|---------------|
| New theme | Add entry in `ThemeSelector.jsx` |
| New export format | Extend `exportHelper.js` |
| New frame SVG | Add SVG to `public/frames/` and update `canvasEngine.js` |
| New preview layout | Add widget in `Telor-View/lib/widgets/` |
| Bridge action | Add handler in `websocket_server.py` + client method in `useTelorBridge.js` |
