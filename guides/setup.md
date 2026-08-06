# Setup Guide

## Prerequisites

| Tool | Version | For |
|------|---------|-----|
| Python | 3.10+ | Telor Bridge |
| Node.js | 18+ | Telor Web |
| Flutter | 3.x | Telor View |
| ADB | Latest | Android device connection |

## Telor Bridge

```bash
cd Telor-Bridge
python -m venv venv
venv\Scripts\activate      # Windows
# source venv/bin/activate # Mac/Linux
pip install -r requirements.txt

# Run server mode
python -m bridge.main

# Or single capture
python -m bridge.main capture
```

## Telor Web

```bash
cd Telor-Web
npm install
npm run dev
# Opens at http://localhost:5173
```

## Telor View

```bash
cd Telor-View
flutter pub get
flutter run
# Select connected Android device or emulator
```

## Verify Connection

1. Start Bridge server: `python -m bridge.main` (listens on ws://localhost:7700)
2. Start Web: `npm run dev`
3. Open Web in browser — should show "Bridge Connected" badge in editor
4. Click "Capture from Device" to test
