# Bridge WebSocket Protocol

**Endpoint:** `ws://localhost:7700`

## Client → Server (Actions)

### `ping`
```json
{ "action": "ping" }
```
Response: `{ "type": "pong" }`

### `capture_single`
```json
{ "action": "capture_single" }
```
Response:
```json
{
  "type": "screenshot",
  "path": "output/screenshot_0001.png",
  "session": { "app": "Captured App", "screens": ["screenshot_0001.png"], "version": "1.0" }
}
```

### `capture_batch`
```json
{ "action": "capture_batch", "count": 5, "app": "My App", "tagline": "Optional tagline" }
```
Response:
```json
{
  "type": "batch_result",
  "paths": ["output/batch_0001.png", "..."],
  "session": { "app": "My App", "screens": ["batch_0001.png", "..."], "version": "1.0" }
}
```

### `crawl`
Auto-navigate app via Appium and capture sequential screenshots.
```json
{ "action": "crawl", "package": "com.example.app", "max_screens": 20, "app": "My App" }
```
Response:
```json
{
  "type": "crawl_result",
  "paths": ["output/crawl_0001.png", "..."],
  "session": { "app": "My App", "screens": ["crawl_0001.png", "..."] }
}
```

### `get_session`
```json
{ "action": "get_session" }
```
Response: `{ "type": "session", "session": { ... } }`

### `list_devices`
```json
{ "action": "list_devices" }
```
Response:
```json
{
  "type": "devices",
  "usb": [{ "serial": "ABCD1234", "model": "Pixel 7" }],
  "wifi": [{ "serial": "192.168.1.5:5555", "transport": "wifi" }]
}
```

### `connect_wifi`
```json
{ "action": "connect_wifi", "ip": "192.168.1.5", "port": 5555 }
```
Response: `{ "type": "connect_result", "success": true }`

## Error Response
```json
{ "type": "error", "message": "Unknown action: ..." }
```

## CLI Equivalents

| WebSocket action | CLI command |
|-----------------|-------------|
| capture_single | `python -m bridge.main capture --app "My App"` |
| capture_batch | `python -m bridge.main batch --count 5` |
| crawl | `python -m bridge.main crawl --package com.example.app` |
| server | `python -m bridge.main server` |
