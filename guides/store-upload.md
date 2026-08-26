# Store upload (Play / App Store)

Glint exports **PNG ZIP** files. Upload is still manual (or Fastlane) — soft launch does not call Google/Apple APIs.

## Google Play Console

1. Export Play phone preset ZIP from Glint Web (`1080×1920`, store `play/phone`).
2. Play Console → Your app → Store presence → Main store listing → Phone screenshots.
3. Upload PNGs in order (`screen_1` = first listing tile).
4. Repeat per device slot as needed (7″ / 10″ tablet, TV, Wear, Chromebook) using the matching template.

## App Store Connect

1. Export iPhone (`ios/iphone`) or iPad (`ios/ipad`) preset ZIP.
2. App Store Connect → your version → App Preview and Screenshots.
3. Drop PNGs into the correct device size well (6.7" / 12.9").

## Fastlane

1. Export with **Fastlane** ZIP layout (or `glint_export` / headless `--layout fastlane`).
2. Unzip into your app’s `fastlane/screenshots/` (or merge `phoneScreenshots/`).
3. Run `fastlane deliver` / `supply` as usual.

Example after unzip:

```
fastlane/screenshots/phoneScreenshots/en-US/screen_1.png
```

## Locales

`session.json` may include `locales: ["en-US", …]`. Soft launch ships **one locale** folder in Fastlane ZIPs (`en-US` default). Multi-locale caption packs are Phase C.

## Compliance

Screenshots must show **real app UI**. Glint Capture / Bridge produce real pixels — do not replace them with AI-fabricated mockups before upload.
