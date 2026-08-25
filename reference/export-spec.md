# Export Specification

## Output Format

- **Format:** PNG (lossless)
- **Batch:** ZIP archive containing individual PNGs

## Store Presets

| Store | Resolution | Aspect | Max file size |
|-------|-----------|--------|---------------|
| Play Store (phone) | 1080 × 1920 | 9:16 | ≤ 8 MB |
| App Store (phone) | 1290 × 2796 | ~9:19.5 | ≤ 8 MB |
| App Store (tablet) | 2048 × 2732 | 4:3 | ≤ 8 MB |
| Play feature graphic | 1024 × 500 | ~2:1 | ≤ 8 MB |

## File Naming

### Flat (default)

- Batch export: `screen_1.png`, `screen_2.png`, … (or `ios_screen_N` / `ipad_screen_N`)
- ZIP name: `{AppName}.zip` or `glint.zip`

### Fastlane layout (optional)

```
phoneScreenshots/en-US/screen_1.png
phoneScreenshots/en-US/screen_2.png
…
```

iPad uses `tabletScreenshots/{locale}/…`. Feature graphic uses `featureGraphic/{locale}/…`.

Enable in Glint Web export panel (**ZIP layout → Fastlane**) or headless `--layout fastlane --locale en-US`.

## Play Store Requirements

| Requirement | Value |
|-------------|-------|
| Min dimension | 320 px |
| Max dimension | 3840 px |
| Aspect ratio | Between 2:1 and 1:2 |
| File size | ≤ 8 MB per screenshot |
| Recommended phone | 1080 × 1920 |
| Feature graphic | 1024 × 500 |

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
