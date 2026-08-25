# Golden path (soft launch)

**Goal:** first store ZIP in under 15 minutes. One device only.

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
# Edit rules for 3–5 real screens (home, feature, settings…)
# Soft launch: capture pixel9 only
glint capture
```

Output folder (default `glint_screenshots/`): PNGs + `session.json`.

## 2. Web

```bash
# Local
cd Glint-Web && npm install && npm run dev
# Or open the hosted soft-launch URL from the org README
```

1. **Import** the Capture folder (or drag `session.json` + PNGs)
2. Pick template **Blink** or **Warm Glow** (Play)
3. Tweak captions / Colors / Design chrome if needed
4. **Export ZIP**

## 3. View (optional QA)

1. In Web → **Copy for Glint View**
2. Open Glint View on a phone → Paste Session
3. Confirm listing preview looks right

## 4. Upload

Upload ZIP PNGs to Play Console / App Store Connect. Prefer **real UI only** — never invent screens.
