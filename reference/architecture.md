# Architecture

```
         ┌──────────────────────────────┐
         │   TELOR CAPTURE (Public)      │
         │   Flutter package + CLI       │
         │   Golden screenshot rules     │
         └────────────┬─────────────────┘
                      │ session.json + PNGs
                      ▼
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
         │   Templates + batch export   │
         │   AdSense revenue layer      │
         └────────────┬─────────────────┘
                      │ QR / session JSON
                      ▼
         ┌──────────────────────────────┐
         │   TELOR VIEW (Private)        │
         │   Flutter + AdMob            │
         │   Play / App Store preview   │
         └──────────────────────────────┘
```

## Capture Paths

| Path | Tool | Requires Device |
|------|------|-----------------|
| Code-based | `telor_capture` Flutter package | No |
| Device-based | Telor Bridge (ADB) | Yes (Android) |
| Manual | Upload to Telor Web | No |

## Data Flow

1. **Capture** — `telor_capture` generates PNGs via golden tests, OR Bridge captures via ADB
2. **Session** — Both paths emit `session.json` with ordered screenshot list
3. **Design** — Web imports session, applies viral template to all screens, batch exports
4. **Preview** — View loads session JSON (QR scan or paste), renders store-style preview

## Monetization

| Layer | Method |
|-------|--------|
| Telor Web | Google AdSense (banner + interstitial) |
| Telor View | Google AdMob (AppOpen ad on launch) |
| Telor Bridge | OSS — drives ecosystem traffic |
| Telor Capture | OSS pub.dev package — drives ecosystem traffic |
