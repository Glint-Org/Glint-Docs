# Session JSON Schema

Used to transfer screenshot sessions between Glint-Capture / Bridge → Web → View.

## Format

```json
{
  "screens": [
    "android/pixel9/home.png",
    "android/pixel9/profile.png"
  ],
  "store": "play/phone",
  "version": "1.0",
  "locales": ["en-US"],
  "exportedAt": "2026-06-30T12:00:00.000Z"
}
```

For Glint Web frames, Capture writes **one primary device** in `screens` (e.g. `pixel9` for Play). Other device folders may exist on disk. Soft-launch tip: capture a single device.

## Fields

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `screens` | string[] | yes | Ordered list of screenshot filenames or data URLs |
| `store` | string | yes | Platform/device target. Canonical: `play/phone`, `play/tablet-7`, `play/tablet-10`, `play/tv`, `play/wear`, `play/chromebook`, `ios/iphone`, `ios/ipad` |
| `locales` | string[] | no | BCP-47 tags for Fastlane folders (default `["en-US"]`) |
| `version` | string | yes | Schema version |
| `exportedAt` | string (ISO) | yes | Export timestamp |

## Transport

- **Glint-Capture → Web:** Folder import (`session.json` + PNGs). Screen paths are relative, e.g. `android/pixel9/home.png`.
- **Bridge → Web:** WebSocket (after pairing) with `data_url` / `data_urls` plus session payload, or local `output/session.json`
- **Web → View:** Prefer **Copy for Glint View** after Preview/Export. `screens` should be `data:image/...` or `http(s)` URLs. Filenames alone will not load on device. QR encodes compact metadata only (PNG payloads are too large).

## Producers

| Producer | Writes `session.json`? | `store` format | Notes |
|----------|------------------------|----------------|-------|
| Glint-Capture | Yes | `play/phone`, `ios/iphone`, `ios/ipad` | After all screenshots; `screens` list relative paths |
| Glint-Bridge | Yes | `play/phone` (default) | On capture / batch / crawl / server |
| Glint-Web | Yes (clipboard) | Pass-through | View paste embeds rendered frame data URLs |
