# Architecture

```
         ┌──────────────────────────────┐
         │   GLINT CAPTURE (Public)      │
         │   Flutter package + CLI       │
         │   Golden screenshot rules     │
         └────────────┬─────────────────┘
                      │ session.json + PNGs
                      ▼
         ┌──────────────────────────────┐
         │   GLINT BRIDGE (Public)       │
         │   ADB + Appium + crawler     │
         │   Python CLI + WebSocket     │
         └────────────┬─────────────────┘
                      │ ws://localhost:7700
                      ▼
         ┌──────────────────────────────┐
         │   GLINT WEB (Public)          │
         │   React + Vite + Fabric.js   │
         │   Templates + batch export   │
         │   AdSense revenue layer      │
         └────────────┬─────────────────┘
                      │ QR / session JSON
                      ▼
         ┌──────────────────────────────┐
         │   GLINT VIEW (Private)        │
         │   Flutter + AdMob            │
         │   Play / App Store preview   │
         └──────────────────────────────┘
```

## Capture Paths

| Path | Tool | Requires Device |
|------|------|-----------------|
| Code-based | `glint_capture` Flutter package | No |
| Device-based | Glint Bridge (ADB) | Yes (Android) |
| Manual | Upload to Glint Web | No |

## Data Flow

1. **Capture** — `glint_capture` generates PNGs via golden tests, OR Bridge captures via ADB
2. **Session** — Both paths emit `session.json` with ordered screenshot list
3. **Design** — Web imports session, applies viral template to all screens, batch exports
4. **Preview** — View loads session JSON (QR scan or paste), renders store-style preview

## Monetization

| Layer | Method |
|-------|--------|
| Glint Web | Google AdSense (banner + interstitial) |
| Glint View | Google AdMob (AppOpen ad on launch) |
| Glint Bridge | OSS — drives ecosystem traffic |
| Glint Capture | OSS pub.dev package — drives ecosystem traffic |
