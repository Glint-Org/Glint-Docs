# Export Specification

## Output Format

- **Format:** PNG (lossless)
- **Batch:** ZIP archive containing individual PNGs

## Store Presets

Canonical key: `{platform}/{device}` (e.g. `play/phone`, `ios/ipad`).

| Platform | Device | Key | Resolution |
|----------|--------|-----|------------|
| Play Store | Phone | `play/phone` | 1080 × 1920 |
| Play Store | 7″ Tablet | `play/tablet-7` | 1200 × 1920 |
| Play Store | 10″ Tablet | `play/tablet-10` | 1600 × 2560 |
| Play Store | TV | `play/tv` | 1920 × 1080 |
| Play Store | Wear OS | `play/wear` | 450 × 450 |
| Play Store | Chromebook | `play/chromebook` | 1920 × 1080 |
| App Store | iPhone | `ios/iphone` | 1290 × 2796 |
| App Store | iPad | `ios/ipad` | 2048 × 2732 |

Legacy aliases: `play` → `play/phone`, `ios` → `ios/iphone`, `ios-tablet` → `ios/ipad`.

## File Naming

### Flat (default)

- Batch export: `screen_1.png`, `ios_screen_N`, `tv_screen_N`, …
- ZIP name: `{AppName}.zip` or `glint.zip`

### Fastlane layout (optional)

```
phoneScreenshots/en-US/screen_1.png
sevenInchScreenshots/en-US/tablet7_screen_1.png
tenInchScreenshots/en-US/tablet10_screen_1.png
tvScreenshots/en-US/tv_screen_1.png
wearOsScreenshots/en-US/wear_screen_1.png
tabletScreenshots/en-US/ipad_screen_1.png
```

Enable in Glint Web export panel (**ZIP layout → Fastlane**) or headless `--layout fastlane --locale en-US`.

## Play Store Requirements

| Requirement | Value |
|-------------|-------|
| Min dimension | 320 px |
| Max dimension | 3840 px |
| Aspect ratio | Between 2:1 and 1:2 |
| File size | ≤ 8 MB per screenshot |
| Recommended phone | 1080 × 1920 |

## App Store Requirements

| Requirement | Value |
|-------------|-------|
| iPhone 6.7" | 1290 × 2796 |
| iPad Pro 12.9" | 2048 × 2732 |
| Format | PNG or JPEG |
| File size | ≤ 8 MB per screenshot |

## Capture paths

- glint_capture output: nested paths e.g. `android/pixel9/home.png`

## Session Export (Glint View)

After Preview or ZIP export in Glint Web:

1. **Copy for Glint View** — clipboard JSON with full `data:` screens (recommended)
2. **QR** — compact app/tagline/store metadata only; use paste for images

View is preview-only; it does not edit frames.
