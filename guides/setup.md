# Setup Guide

## Prerequisites

| Tool | Version | For |
|------|---------|-----|
| [FVM](https://fvm.app) | Latest | Flutter version management |
| Flutter | **3.44.1** (via FVM) | Glint View, Glint Capture |
| Python | 3.10+ | Glint Bridge |
| Node.js | 18+ | Glint Web |
| ADB | Latest | Android device connection (Bridge) |

## FVM Setup (Flutter projects)

All Flutter apps and packages use **FVM 3.44.1**:

```bash
# Install FVM (once)
dart pub global activate fvm

# Glint View
cd Glint-View
fvm use 3.44.1
fvm flutter pub get

# Glint Capture
cd Glint-Capture
fvm use 3.44.1
fvm flutter pub get

# Example app
cd Glint-Capture/example
fvm use 3.44.1
fvm flutter pub get
```

Android builds use **Gradle 8.14**, **targetSDK 36**, and **16KB page alignment** for modern device compatibility.

## Glint Capture (Flutter - no device needed)

```bash
cd Glint-Capture/example
fvm flutter pub get

# Initialize (from an app that depends on glint_capture)
glint init          # creates glint.yaml + test/glint_screenshots_test.dart
glint capture       # runs flutter test + writes PNGs and session.json

# Or run the screens test directly
fvm flutter test test/glint_screenshots_test.dart
```

Output: `glint_screenshots/` (or path from `glint.yaml`) containing nested device PNGs **and** `session.json` (schema v1).

## Glint Bridge (Android device capture)

```bash
cd Glint-Bridge
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate
pip install -r requirements.txt

python glint.py check
python glint.py devices
python glint.py capture
python glint.py batch 5
python glint.py crawl com.example.app   # requires Appium
python glint.py start                   # WebSocket on 127.0.0.1:7700 + pairing token
```

Output: `output/session.json` + PNGs

Note the **pairing token** printed by `start`. Enter it in Glint-Web before live capture.

## Glint Web

```bash
cd Glint-Web
npm install
npm run dev
# Opens at http://localhost:5173
```

1. Import session folder or upload screenshots
2. Pick a curated store template
3. Customize on the canvas (text, background, frames)
4. Batch export ZIP
5. Optional: scan QR with Glint View

## Glint View

```bash
cd Glint-View
fvm flutter pub get
fvm flutter run
```

- Scan QR from Glint Web export
- Or paste session JSON manually

## Verify End-to-End

1. `cd Glint-Capture/example && glint capture` (or `fvm flutter test …`)
2. Confirm `session.json` exists next to the PNGs
3. `cd Glint-Web && npm run dev` → import the output folder
4. Pick template → Export ZIP
5. `cd Glint-View && fvm flutter run` → scan QR or paste JSON

## Optional: Bridge + Web live capture

1. `python glint.py start` - copy the pairing token
2. `npm run dev` in Glint-Web
3. Enter token in the editor → Pair → Capture from Device
