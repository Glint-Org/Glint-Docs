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
Response: `{ "type": "screenshot", "path": "output/screenshot_0001.png" }`

### `capture_batch`
```json
{ "action": "capture_batch", "count": 5 }
```
Response: `{ "type": "batch_result", "paths": ["output/batch_0001.png", ...] }`

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
