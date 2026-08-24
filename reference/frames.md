# Device Frames

SVG-based device frames are stored in `Glint-Web/public/frames/`.

Screen insets for compositing live in `Glint-Web/src/utils/frameMeta.js`.

## Supported Devices

| Frame | File | Notes |
|-------|------|-------|
| Pixel 7 | `pixel7.svg` | Play Store default |
| Samsung Galaxy S23 | `galaxy-s23.svg` | Play Store |
| Samsung M12 | `samsung-m12.svg` | Play Store |
| Generic Android | `generic.svg` | Fallback |
| iPhone 15 | `iphone15.svg` | App Store |
| iPhone 14 Pro | `iphone14-pro.svg` | App Store |
| iPad Pro | `ipad-pro.svg` | App Store tablet |
| iPad 10 | `ipad-10.svg` | App Store tablet |

## Adding a Frame

1. Export device bezel as SVG at the device’s logical aspect (not full store canvas)
2. Punch out the screen with `fill-rule="evenodd"` so the display area is transparent
3. Place in `public/frames/`
4. Add insets (`top/right/bottom/left/rx/width/height`) in `frameMeta.js`
5. Register in `FrameSelector.jsx`

## Frame Requirements

- ViewBox matches the physical device aspect (e.g. 390×844 for iPhone)
- Bezel only - screen region must be transparent (evenodd hole)
- Outer bezel = device color
- Optional drop shadow via SVG filter
- No external dependencies or embedded raster images

## Template Usage

Prefer the `device` layer - it composites the screenshot **inside** the frame:

```json
{ "type": "device", "frame": "iphone15", "slot": 0, "scale": 0.58, "position": "center", "marginTop": 480 }
```

Legacy separate layers (`screenshot` + `device-frame`) still work but do not clip the shot into the bezel.
