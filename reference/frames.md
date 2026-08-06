# Device Frames

SVG-based device frames are stored in `Telor-Web/public/frames/`.

## Supported Devices

| Frame | File | Notes |
|-------|------|-------|
| Pixel 7 | `pixel7.svg` | Recommended default |
| Samsung Galaxy S23 | `galaxy-s23.svg` | |
| Generic Android | `generic.svg` | Fallback |

## Adding a Frame

1. Export device frame as SVG (from Figma, Sketch, or similar)
2. Remove background — keep only the bezel/cutout
3. Set viewBox to match 1080×1920 canvas coordinates
4. Place in `public/frames/`
5. Restart dev server

## Frame Requirements

- ViewBox should match the screenshot area
- Inner transparent region = visible screenshot area
- Outer bezel = any color (usually black or device color)
- No external dependencies or embedded raster images
