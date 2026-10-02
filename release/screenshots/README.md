# Screenshots

The Mac App Store accepts a 16:10 image at one of these sizes: **1280×800, 1440×900, 2560×1600, 2880×1800**. Supply 1–10 of them (PNG or JPEG, no transparency).

## Generate them

In the app repository, run:

```sh
scripts/screenshots.sh
```

It writes four pictures to `build/screenshots/` (2880×1800 on a Retina display, 1440×900 otherwise):

| File | Shows |
|---|---|
| `01-clipboard-history.png` | The shelf panel with mixed cards (code, link, image, note, color), dark |
| `02-list-and-preview.png` | List layout with the apps sidebar and highlighted code in the preview, light |
| `03-quick-paste.png` | Settings ▸ Quick Paste and the Quick Paste overlay, dark |
| `04-privacy.png` | Settings ▸ Privacy, light |

The app draws its own views into the files, using a made-up history that lives in memory. It doesn't capture the screen, and it doesn't read your clipboard, history or settings, so nothing personal can appear. Four demo windows show on screen for a couple of seconds each while they are drawn.

## Shot list for manual captures

If you want more than the generated four:

1. The shelf panel over a code editor, showing mixed cards (code, link, image, color)
2. Search in action: typing "json" with the matching code highlighted
3. Apps sidebar with one app selected (grouping by source app)
4. List layout with the detail pane showing highlighted code with line numbers
5. The "Paste As" menu (transforms)
6. Pinboards: color-coded chips with a pinned item
7. Settings ▸ Fonts and Settings ▸ Appearance (image background)
8. The privacy screen: excluded apps and concealed-content toggle

Tips:
- Use the seeded demo data: launch with `-PasteMeUITesting -PasteMeSeed -PasteMeShow panel`.
- Use a clean desktop, one wallpaper, light mode for 1–4 and dark mode for 5–8.
