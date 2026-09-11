# Device Frames

Curated set only - the frames developers use most for Play and App Store. No long device catalog.

SVGs: `Glint-Web/public/frames/`  
Insets: `Glint-Web/src/utils/frameMeta.js`  
Capture: `Glint-Capture/lib/src/devices.dart` (`GLINTDevices.premium`)

## Devices

| Frame | Web file | Capture name | Logical size | Store |
|-------|----------|--------------|--------------|-------|
| Pixel 9 | `pixel9.svg` | `pixel9` | 412×915 @2.625 | Play default |
| Galaxy S24 | `galaxy-s24.svg` | `galaxy_s24` | 360×780 @3 | Play |
| iPhone 16 Pro Max | `iphone16-pro-max.svg` | `iphone16_pro_max` | 430×932 @3 | App Store 6.7" |
| iPhone 16 Pro | `iphone16-pro.svg` | `iphone16_pro` | 393×852 @3 | App Store |
| iPad Pro 13" | `ipad-pro-13.svg` | `ipad_pro_129` | 1024×1366 @2 | Tablet |
| iPad Pro 11" | `ipad-pro.svg` | `ipad_pro_11` | 834×1194 @2 | Tablet |

Web also allows **None** (rounded screenshot, no bezel). Custom SVG upload remains available in FramePicker.

## Adding a frame (rare)

1. SVG bezel with evenodd screen hole → `public/frames/`
2. Insets in `frameMeta.js` + option in `FrameSelector.jsx`
3. Matching `GLINTDevice` in Capture `devices.dart`

## Template usage

```json
{ "type": "device", "frame": "iphone16-pro-max", "slot": 0, "scale": 0.58, "position": "center" }
```
