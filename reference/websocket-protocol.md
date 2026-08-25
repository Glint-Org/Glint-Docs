# Bridge WebSocket Protocol

**Endpoint:** `ws://127.0.0.1:7700` (localhost only)

The Bridge server binds to **loopback** and requires a **pairing token** before any capture actions are accepted.

## Pairing (required first message)

When you start the server (`python glint.py start` or `python -m bridge.main server`), the console prints a short hex token.

**Client → Server (first message):**
```json
{ "action": "pair", "token": "<token-from-console>" }
```

**Success:**
```json
{ "type": "paired", "success": true }
```

**Failure:** connection closed with code `1008` (Unauthorized) and optional error payload:
```json
{ "type": "error", "message": "Invalid pairing token. Request denied." }
```

Glint-Web stores the token in `localStorage` (`glint_bridge_token`) and re-sends it on reconnect.

---

## Client → Server (Actions)

All actions below require a successful pair.

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
  "data_url": "data:image/png;base64,...",
  "session": { "app": "Captured App", "screens": ["screenshot_0001.png"], "version": "1.0" }
}
```

`data_url` is required for Glint Web to display the shot in-browser. `path` remains for disk/CLI use.

### `capture_batch`
```json
{ "action": "capture_batch", "count": 5, "app": "My App", "tagline": "Optional tagline" }
```
Response:
```json
{
  "type": "batch_result",
  "paths": ["output/batch_0001.png", "..."],
  "data_urls": ["data:image/png;base64,...", "..."],
  "session": { "app": "My App", "screens": ["batch_0001.png", "..."], "version": "1.0" }
}
```

### `crawl`
Auto-navigate app via Appium and capture sequential screenshots (optional dependency).
```json
{ "action": "crawl", "package": "com.example.app", "max_screens": 20, "app": "My App" }
```
Response:
```json
{
  "type": "crawl_result",
  "paths": ["output/crawl_0001.png", "..."],
  "data_urls": ["data:image/png;base64,...", "..."],
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
| (start + token) | `python glint.py start` |
| capture_single | `python glint.py capture` |
| capture_batch | `python glint.py batch 5` |
| crawl | `python glint.py crawl com.example.app` |
| list_devices | `python glint.py devices` |
