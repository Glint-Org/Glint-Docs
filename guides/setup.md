# Setup Guide

## Quick start (soft launch)

1. Add Capture (`ref: v0.1.0` git dep) → `glint init` → write real-screen rules → `glint capture` (**pixel9** only).  
2. Open Glint Web (`npm run dev` or hosted URL) → Import folder → Blink / Warm Glow → Export ZIP.  
3. Optional: Copy for Glint View → paste on device.

Full walkthrough: [golden-path.md](golden-path.md). Verify: [smoke-checklist.md](smoke-checklist.md).

## Prerequisites

| Tool | Version | For |
|------|---------|-----|
| [FVM](https://fvm.app) | Latest | Flutter version management |
| Flutter | **3.44.1** (via FVM) | Glint View, Glint Capture |
| Python | 3.10+ | Glint Bridge |
| Node.js | 18+ | Glint Web |
| ADB | Latest | Android device connection (Bridge) |

## FVM Setup (Flutter projects)

```bash
dart pub global activate fvm

cd Glint-View && fvm use 3.44.1 && fvm flutter pub get
cd Glint-Capture && fvm use 3.44.1 && fvm flutter pub get
cd Glint-Capture/example && fvm use 3.44.1 && fvm flutter pub get
```

## Glint Capture

```bash
# In your Flutter app pubspec:
#   glint_capture:
#     path: ../Glint-Capture   # or git URL

dart pub global activate --source path /path/to/Glint-Capture
glint init
glint capture
```

Output: `glint_screenshots/` (or `glint.yaml` path) with nested PNGs **and** `session.json`.

## Glint Bridge

```bash
cd Glint-Bridge
python -m venv venv && source venv/bin/activate
pip install -r requirements.txt

python glint.py check
python glint.py devices
python glint.py capture          # or batch / start
# crawl needs Appium — optional; see Bridge README
python glint.py start            # ws://127.0.0.1:7700 + pairing token
```

Live Web captures include **data URLs** for browser display. Server is **loopback-only**.

## Glint Web

```bash
cd Glint-Web && npm install && npm run dev
# http://localhost:5173
```

1. Import session folder or upload screenshots
2. Pick a template pack → frames board
3. Edit → Export ZIP
4. Preview → **Copy for Glint View** (full screens for paste)

## Glint View (preview only)

```bash
cd Glint-View
fvm flutter pub get
fvm flutter run
```

- **Paste Session JSON** from Web (recommended for screenshots)
- QR is useful for metadata; image payloads use paste

## Verify End-to-End

1. Capture (example or your app) → confirm `session.json`
2. Web → import → template → Export ZIP
3. Copy for Glint View → View → Paste → store listing preview

## Optional: Bridge + Web live capture

1. `python glint.py start` — copy pairing token
2. Web → pair → Capture from Device
