# Golden path

Get your first store ZIP in under 15 minutes. Start with one device.

## 1. Capture (Flutter)

```yaml
# pubspec.yaml
dev_dependencies:
  glint_capture:
    git:
      url: https://github.com/Glint-Org/Glint-Capture.git
      ref: v0.1.0
```

```bash
dart pub get
dart pub global activate --source git https://github.com/Glint-Org/Glint-Capture.git
glint init
# Edit rules for 3-5 real screens (home, feature, settings…)
# Tip: capture pixel9 only until you are comfortable
glint capture
```

Output folder (default `glint_screenshots/`): PNGs + `session.json`.

## 2. Web

```bash
cd Glint-Web && npm install && npm run dev
```

Or open the hosted Glint Web URL when you have one.

1. **Import** the Capture folder (or drag `session.json` + PNGs)  
2. Pick a template (for example **Blink** or **Warm Glow** on Play)  
3. Tweak captions, colors, or device chrome if you want  
4. **Export ZIP**  

## 3. View (optional QA)

1. In Web → **Copy for Glint View**  
2. Open Glint View on a phone → Paste Session  
3. Confirm the listing preview looks right  

## 4. Upload

Upload the ZIP PNGs to Play Console or App Store Connect. Use **real app UI only** - never invent screens.
