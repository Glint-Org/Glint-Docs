# Project Structure

```
Telor-Org/
├── plan.md                          # Master plan & strategy
├── Telor-Bridge/                    # Public - Capture engine (Python)
│   ├── bridge/
│   │   ├── main.py                  # CLI entry point
│   │   ├── adb_usb.py              # USB ADB device management
│   │   ├── adb_wifi.py             # WiFi ADB connection
│   │   ├── capture.py              # Screenshot capture engine
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
│   │   │   ├── FrameEditor.jsx     # Canvas wrapper
│   │   │   ├── ThemeSelector.jsx   # Background theme picker
│   │   │   ├── ExportManager.jsx   # PNG/ZIP export
│   │   │   └── AdSlot.jsx          # AdSense placeholder
│   │   ├── hooks/
│   │   │   └── useTelorBridge.js   # WebSocket client hook
│   │   ├── utils/
│   │   │   ├── canvasEngine.js     # Fabric.js operations
│   │   │   └── exportHelper.js     # Download helpers
│   │   ├── pages/
│   │   │   ├── Home.jsx            # Upload landing page
│   │   │   └── Editor.jsx          # Canvas editor page
│   │   ├── main.jsx                # App entry + routing
│   │   └── index.css               # Tailwind import
│   ├── public/frames/              # Device frame SVGs
│   └── vite.config.js
│
├── Telor-View/                      # Private - Preview app (Flutter)
│   ├── lib/
│   │   ├── main.dart               # App entry + routes
│   │   ├── screens/
│   │   │   ├── home.dart           # Landing screen
│   │   │   ├── scanner.dart        # QR scanner
│   │   │   └── preview.dart        # Store preview
│   │   ├── widgets/
│   │   │   ├── listing_header.dart # App icon + name + rating
│   │   │   └── screenshot_carousel.dart  # Swipeable carousel
│   │   └── services/
│   │       └── session_loader.dart # JSON/URL/file loader
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
