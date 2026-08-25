# Project Structure

```
Glint-Org/
├── glint-master-plan.md             # Master plan & strategy
├── Glint-Capture/                   # Public - Flutter screenshot package
│   ├── lib/
│   │   ├── glint_capture.dart       # Public API
│   │   └── src/
│   │       ├── devices.dart         # Device presets
│   │       ├── rules.dart           # GLINTRule, templates
│   │       ├── runner.dart          # Capture orchestration + session.json
│   │       ├── session.dart         # session.json writer
│   │       └── pump.dart            # Pump helpers
│   ├── bin/glint.dart               # CLI: init / capture
│   ├── example/                     # Sample app + rules
│   └── test/
│
├── Glint-Bridge/                    # Public - Capture engine (Python)
│   ├── glint.py                     # Simple CLI entry
│   ├── bridge/
│   │   ├── main.py                  # CLI entry point
│   │   ├── adb_usb.py              # USB ADB device management
│   │   ├── adb_wifi.py             # WiFi ADB connection
│   │   ├── capture.py              # Screenshot capture engine
│   │   ├── session.py              # session.json generation
│   │   ├── crawler.py              # Appium auto-crawl (optional)
│   │   └── websocket_server.py     # Localhost :7700 + pairing token
│   ├── scripts/
│   ├── output/                     # Screenshot output directory
│   └── requirements.txt
│
├── Glint-Web/                       # Frames editor (React)
│   ├── src/
│   │   ├── components/
│   │   │   ├── FrameBoard.jsx / FrameCanvas.jsx
│   │   │   ├── FramesPanel.jsx / AssetsPanel.jsx / ExportPanel.jsx
│   │   │   ├── TemplateGallery.jsx
│   │   │   ├── QRExporter.jsx      # Copy for Glint View + QR metadata
│   │   │   ├── SessionImporter.jsx # Folder / paste import
│   │   │   └── …
│   │   ├── hooks/
│   │   │   ├── useFrames.js
│   │   │   └── useGlintBridge.js   # prefers data_url(s)
│   │   ├── pages/
│   │   │   ├── Home.jsx
│   │   │   └── Editor.jsx          # Frames board editor
│   │   └── …
│   ├── public/
│   │   ├── frames/                 # Device bezel SVGs
│   │   └── templates/              # Play / App Store / iPad packs
│   └── vite.config.js
│
├── Glint-View/                      # Store listing preview only (Flutter)
│   └── lib/ …
│
└── Glint-Docs/                      # Reference docs
    ├── guides/
    │   ├── setup.md
    │   └── workflow.md
    └── reference/
        ├── architecture.md
        ├── websocket-protocol.md   # Includes pairing
        ├── session-schema.md
        ├── export-spec.md
        ├── frames.md
        └── project-structure.md
```
