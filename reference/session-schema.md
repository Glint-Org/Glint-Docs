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

- **Glint-Capture → Web:** Folder drag (session.json + PNGs in same directory)
- **Bridge → Web:** WebSocket message with session payload, or local `output/session.json`
- **Web → View:** QR code (encoded JSON), clipboard paste, or file drop
