# Device Frames

SVG-based device frames are stored in `Glint-Web/public/frames/`.

## Supported Devices

| Frame | File | Notes |
|-------|------|-------|
| Pixel 7 | `pixel7.svg` | Play Store default |
| Samsung Galaxy S23 | `galaxy-s23.svg` | Play Store |
| Generic Android | `generic.svg` | Fallback |
| iPhone 15 | `iphone15.svg` | App Store |
| iPad Pro | `ipad-pro.svg` | App Store tablet |

## Adding a Frame

1. Export device frame as SVG (from Figma, Sketch, or similar)
2. Remove background — keep only the bezel/cutout
3. Set viewBox to match 1080×1920 canvas coordinates
4. Place in `public/frames/`
5. Register in `FrameSelector.jsx` and template JSON files

## Frame Requirements

- ViewBox should match the screenshot area
- Inner transparent region = visible screenshot area
- Outer bezel = any color (usually black or device color)
- No external dependencies or embedded raster images

## Template Usage

Templates reference frames by ID in their JSON layer definitions:

```json
{ "type": "device-frame", "frame": "iphone15", "position": "center", "scale": 0.75 }
```
