# Session JSON Schema

Used to transfer screenshot sessions between Glint-Capture / Bridge → Web → View.

## Format

```json
{
  "app": "com.example.app",
  "tagline": "Edit Photos Like a Pro",
  "screens": [
    "home_pixel7.png",
    "profile_pixel7.png"
  ],
  "store": "play",
  "version": "1.0",
  "exportedAt": "2026-06-30T12:00:00.000Z"
}
```

## Fields

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `app` | string | yes | App name or package ID |
| `tagline` | string | no | Short marketing tagline |
| `screens` | string[] | yes | Ordered list of screenshot filenames or URLs |
| `store` | string | no | Store target: `play`, `ios`, or `ios-tablet` (default: `play`) |
| `version` | string | yes | Schema version |
| `exportedAt` | string (ISO) | yes | Export timestamp |

## Transport

- **Glint-Capture → Web:** Folder import (`session.json` + PNGs). Capture writes `session.json` automatically after a successful `glint capture` / `flutter test` run (via runner `tearDownAll` and CLI refresh). Screen paths are relative, e.g. `android/pixel7/home.png`.
- **Bridge → Web:** WebSocket (after pairing) with session payload, or local `output/session.json`
- **Web → View:** QR code (encoded JSON), clipboard paste, or file drop

## Producers

| Producer | Writes `session.json`? | Notes |
|----------|------------------------|-------|
| Glint-Capture | Yes | After all screenshots; `screens` list nested paths |
| Glint-Bridge | Yes | On capture / batch / crawl / server |
| Glint-Web | Optional | QR export embeds session metadata for View |
