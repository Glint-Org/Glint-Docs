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

## Glint Capture (Flutter — no device needed)

```bash
cd Glint-Capture/example
fvm flutter pub get

# Run screenshot rules
fvm dart run glint_capture --app ExampleApp --output build/glint_screenshots

# Output: build/glint_screenshots/session.json + PNGs
```

## Glint Bridge (Android device capture)

```bash
cd Glint-Bridge
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate
pip install -r requirements.txt

python -m bridge.main devices
python -m bridge.main capture --app "My App"
python -m bridge.main batch --count 5
python -m bridge.main crawl --package com.example.app   # requires Appium
python -m bridge.main server   # WebSocket on :7700
```

Output: `output/session.json` + PNGs

## Glint Web

```bash
cd Glint-Web
npm install
npm run dev
# Opens at http://localhost:5173
```

1. Import session folder or upload screenshots
2. Pick a viral template
3. Batch export ZIP
4. Scan QR with Glint View

## Glint View

```bash
cd Glint-View
fvm flutter pub get
fvm flutter run
```

- Scan QR from Glint Web export
- Or paste session JSON manually

## Verify End-to-End

1. `cd Glint-Capture/example && fvm dart run glint_capture`
2. `cd Glint-Web && npm run dev` → import `build/glint_screenshots/`
3. Pick template → Export ZIP
4. `cd Glint-View && fvm flutter run` → scan QR or paste JSON

## Optional: Bridge + Web live capture

1. `python -m bridge.main server`
2. `npm run dev` in Glint-Web
3. Editor shows "Bridge Connected" → Capture from Device
