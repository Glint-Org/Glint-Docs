# Session JSON Schema

Used to transfer screenshot sessions between Bridge → Web → View.

## Format

```json
{
  "app": "com.example.app",
  "tagline": "Edit Photos Like a Pro",
  "screens": [
    "home.png",
    "editor.png",
    "profile.png"
  ],
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
| `version` | string | yes | Schema version |
| `exportedAt` | string (ISO) | yes | Export timestamp |

## Transport

- **Bridge → Web:** WebSocket message or local file
- **Web → View:** QR code (encoded JSON or URL), clipboard paste, or file drop
