# Project Structure

```
Glint-Org/
├── plan.md                          # Master plan & strategy
├── Glint-Capture/                   # Public - Flutter screenshot package
│   ├── lib/
│   │   ├── glint_capture.dart       # Public API
│   │   └── src/
│   │       ├── devices.dart         # Device presets
│   │       ├── rules.dart           # GLINTRule, templates
│   │       ├── runner.dart          # Alchemist orchestration
│   │       ├── session.dart         # session.json writer
│   │       └── pump.dart            # Pump helpers
│   ├── bin/glint_capture.dart       # CLI entry
│   ├── example/                     # Sample app + rules
│   └── test/
│
├── Glint-Bridge/                    # Public - Capture engine (Python)
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
├── Glint-Web/                       # Public - Design editor (React)
│   ├── src/
│   │   ├── components/
│   │   │   ├── UploadZone.jsx      # Drag & drop upload
│   │   │   ├── SessionImporter.jsx # Import session.json + PNGs
│   │   │   ├── TemplateGallery.jsx # Viral template picker
│   │   │   ├── BatchProcessor.jsx  # Batch template export
│   │   │   ├── ScreenshotReorder.jsx
│   │   │   ├── QRExporter.jsx      # QR for Glint View
│   │   │   ├── FrameEditor.jsx     # Canvas wrapper
│   │   │   ├── ThemeSelector.jsx   # Background theme picker
│   │   │   ├── ExportManager.jsx   # PNG/ZIP export
│   │   │   └── AdSlot.jsx          # AdSense placeholder
│   │   ├── hooks/
│   │   │   └── useGLINTBridge.js   # WebSocket client hook
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
├── Glint-View/                      # Private - Preview app (Flutter)
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
└── Glint-Docs/                      # Local only - Reference docs
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
