# Glint project pack (`.glint`)

Editable round-trip format between **Glint Web** and **Glint View**.

## Why

| Export | Purpose | Re-editable in Web? |
|--------|---------|---------------------|
| Store PNG ZIP | Play / App Store upload | No (flat art) |
| Copy for Glint View | Quick listing preview (data URLs) | No |
| **`.glint`** | Save project, phone Store Room, reopen in Web | **Yes - pixel-perfect** |

## File shape

ZIP (extension `.glint`):

```
project.json
assets/shots/frame-N.png       # raw screenshots
assets/previews/frame-N.png    # rendered store frames
assets/fabric/frame-N/*.png    # bitmaps from the live canvas
```

`project.json` includes app/tagline/store, editor chrome (background, device frame, styles), template meta, and per-frame `design` + Fabric JSON.

## Web

- **Export** → Download `.glint`
- **Assets** → Open `.glint (editable)`

## View

- **Import `.glint`** → Store Room (previews + keeps pack on device)
- **Share `.glint` to Web** → send file back for more edits

## Policy

Screenshots remain **real UI**. The pack stores editor state; it does not invent marketing art.
