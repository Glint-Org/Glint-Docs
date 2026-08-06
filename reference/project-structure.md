# Project Structure

```
Telor-Org/
├── plan.md                          # Master plan & strategy
├── Telor-Capture/                   # Public - Flutter screenshot package
│   ├── lib/
│   │   ├── telor_capture.dart       # Public API
│   │   └── src/
│   │       ├── devices.dart         # Device presets
│   │       ├── rules.dart           # TelorRule, templates
│   │       ├── runner.dart          # Alchemist orchestration
│   │       ├── session.dart         # session.json writer
│   │       └── pump.dart            # Pump helpers
│   ├── bin/telor_capture.dart       # CLI entry
│   ├── example/                     # Sample app + rules
│   └── test/
│
├── Telor-Bridge/                    # Public - Capture engine (Python)
│   ├── bridge/
│   │   ├── main.py                  # CLI entry point
│   │   ├── adb_usb.py              # USB ADB device management
│   │   ├── adb_wifi.py             # WiFi ADB connection
│   │   ├── capture.py              # Screenshot capture engine
│   │   ├── session.py              # session.json generation
│   │   ├── crawler.py              # Appium auto-crawl (optional)
│   │   └── websocket_server.py     # WebSocket server on :7700
│   ├── scripts/
│   │   ├── install.sh              # Linux/Mac setup
│   │   └── run.bat                 # Windows launcher
│   ├── output/                     # Screenshot output directory
│   └── requirements.txt
│
├── Telor-Web/                       # Public - Design editor (React)
│   ├── src/
│   │   ├── components/
│   │   │   ├── UploadZone.jsx      # Drag & drop upload
│   │   │   ├── SessionImporter.jsx # Import session.json + PNGs
│   │   │   ├── TemplateGallery.jsx # Viral template picker
│   │   │   ├── BatchProcessor.jsx  # Batch template export
│   │   │   ├── ScreenshotReorder.jsx
│   │   │   ├── QRExporter.jsx      # QR for Telor View
│   │   │   ├── FrameEditor.jsx     # Canvas wrapper
│   │   │   ├── ThemeSelector.jsx   # Background theme picker
│   │   │   ├── ExportManager.jsx   # PNG/ZIP export
│   │   │   └── AdSlot.jsx          # AdSense placeholder
│   │   ├── hooks/
│   │   │   └── useTelorBridge.js   # WebSocket client hook
│   │   ├── utils/
│   │   │   ├── canvasEngine.js     # Fabric.js operations
│   │   │   ├── templateEngine.js   # Template rendering
│   │   │   ├── templateLoader.js   # Template JSON loader
│   │   │   └── exportHelper.js     # Download helpers
│   │   ├── pages/
│   │   │   ├── Home.jsx            # Upload + session import
│   │   │   └── Editor.jsx          # Template editor page
│   │   ├── main.jsx                # App entry + routing
│   │   └── index.css               # Tailwind import
│   ├── public/
│   │   ├── frames/                 # Device frame SVGs
│   │   └── templates/              # Viral template JSON definitions
│   └── vite.config.js
│
├── Telor-View/                      # Private - Preview app (Flutter)
│   ├── lib/
│   │   ├── main.dart               # App entry + routes
│   │   ├── screens/
│   │   │   ├── home.dart           # Landing screen
│   │   │   ├── scanner.dart        # QR scanner
│   │   │   └── preview.dart        # Play/App Store preview
│   │   ├── widgets/
│   │   │   ├── listing_header.dart # App icon + name + rating
│   │   │   └── screenshot_carousel.dart
│   │   └── services/
│   │       └── session_loader.dart
│   └── pubspec.yaml
│
└── Telor-Docs/                      # Local only - Reference docs
    ├── README.md
    ├── guides/
    │   ├── setup.md
    │   └── workflow.md
    └── reference/
        ├── architecture.md
        ├── websocket-protocol.md
        ├── session-schema.md
        ├── export-spec.md
        ├── frames.md
        └── project-structure.md
```
