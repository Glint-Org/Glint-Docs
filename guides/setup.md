# Setup Guide

## Prerequisites

| Tool | Version | For |
|------|---------|-----|
| [FVM](https://fvm.app) | Latest | Flutter version management |
| Flutter | **3.44.1** (via FVM) | Telor View, Telor Capture |
| Python | 3.10+ | Telor Bridge |
| Node.js | 18+ | Telor Web |
| ADB | Latest | Android device connection (Bridge) |

## FVM Setup (Flutter projects)

All Flutter apps and packages use **FVM 3.44.1**:

```bash
# Install FVM (once)
dart pub global activate fvm

# Telor View
cd Telor-View
fvm use 3.44.1
fvm flutter pub get

# Telor Capture
cd Telor-Capture
fvm use 3.44.1
fvm flutter pub get

# Example app
cd Telor-Capture/example
fvm use 3.44.1
fvm flutter pub get
```

Android builds use **Gradle 8.14**, **targetSDK 36**, and **16KB page alignment** for modern device compatibility.

## Telor Capture (Flutter — no device needed)

```bash
cd Telor-Capture/example
fvm flutter pub get

# Run screenshot rules
fvm dart run telor_capture --app ExampleApp --output build/telor_screenshots

# Output: build/telor_screenshots/session.json + PNGs
```

## Telor Bridge (Android device capture)

```bash
cd Telor-Bridge
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

## Telor Web

```bash
cd Telor-Web
npm install
npm run dev
# Opens at http://localhost:5173
```

1. Import session folder or upload screenshots
2. Pick a viral template
3. Batch export ZIP
4. Scan QR with Telor View

## Telor View

```bash
cd Telor-View
fvm flutter pub get
fvm flutter run
```

- Scan QR from Telor Web export
- Or paste session JSON manually

## Verify End-to-End

1. `cd Telor-Capture/example && fvm dart run telor_capture`
2. `cd Telor-Web && npm run dev` → import `build/telor_screenshots/`
3. Pick template → Export ZIP
4. `cd Telor-View && fvm flutter run` → scan QR or paste JSON

## Optional: Bridge + Web live capture

1. `python -m bridge.main server`
2. `npm run dev` in Telor-Web
3. Editor shows "Bridge Connected" → Capture from Device
