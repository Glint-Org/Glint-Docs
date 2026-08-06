# Architecture

```
         ┌──────────────────────────────┐
         │   TELOR BRIDGE (Public)       │
         │   ADB + Appium + crawler     │
         │   Python CLI + WebSocket     │
         └────────────┬─────────────────┘
                      │ ws://localhost:7700
                      ▼
         ┌──────────────────────────────┐
         │   TELOR WEB (Public)          │
         │   React + Vite + Fabric.js   │
         │   AdSense revenue layer      │
         └────────────┬─────────────────┘
                      │ QR / session JSON
                      ▼
         ┌──────────────────────────────┐
         │   TELOR VIEW (Private)        │
         │   Flutter + AdMob            │
         │   Store preview on device    │
         └──────────────────────────────┘
```

## Data Flow

1. **Capture** — Bridge connects to Android via ADB (USB/WiFi), captures screenshots
2. **Design** — Web receives images (upload or via Bridge WebSocket), user frames + styles them
3. **Export** — Web generates PNG assets + session JSON (optionally as QR)
4. **Preview** — View loads session JSON (scan QR or paste), renders Play Store–style preview

## Monetization

| Layer | Method |
|-------|--------|
| Telor Web | Google AdSense (banner + interstitial) |
| Telor View | Google AdMob (AppOpen ad on launch) |
| Telor Bridge | OSS — drives ecosystem traffic |
