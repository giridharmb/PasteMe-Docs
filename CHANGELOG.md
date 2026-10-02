# Changelog

## 1.2 — October 2026

The first public release.

### New
- **Quick Paste:** press ⌃⌥V and then 0–9 to paste one of ten saved snippets into any app. A small overlay shows your slots while Paste Me waits. Assign slots in Settings ▸ Quick Paste, from an item's right-click menu, or from the menu bar.
- **Global shortcut controls:**
  - a master switch
  - **Restore Default Shortcuts**
  - a list of apps that keep their own shortcuts (Paste Me steps aside while one is in front)
- **Start at login:** the setting now shows the real macOS state, helps when macOS asks for approval, and is also in the menu bar menu.
- **Privacy Notice in the app:** a summary on the Privacy tab, plus the full notice from Settings, About and the menu bar.

### Mac App Store
- Paste Me can now be built for the Mac App Store. That build runs in the App Sandbox, keeps its data in its own container, and remembers copied files so they can be pasted again after a restart.

### Improved
- **Choosing an item pastes it.** Click an item, or press ↩, and Paste Me switches back to the app you were using and pastes. A single click now does this by default; you can switch back to double-click in Settings ▸ General. If macOS hasn't given Paste Me Accessibility access, a notice explains that the item was copied and how to fix it.
- **Never Save Copies From** now also catches a copy made just before you switch away from an excluded app, and it honors apps that label their copies with `org.nspasteboard.source`. When you exclude an app, Paste Me offers to delete what it already saved from it.

## 1.1 — September 2026 (development build, not released publicly)

### New
- **Apps sidebar:** browse history grouped by the app you copied from. ⌥↑ / ⌥↓ switch apps, ⌘0 shows all apps, ⌘G toggles the sidebar.
- **Paging:** split long histories into pages (100 items per page by default). Use Page Up/Down or ⌘[ / ⌘].
- **Limits:** set the number of items shown in the panel (default 2,000) and the total history size (default 1 GB, oldest items purged first).
- **Fonts:** choose the family and size for interface text, item titles, preview items, preview text and source code.
- **Image previews:** choose the background (checkerboard, transparent, black, white or a custom color). Small images now show at their real size.
- **Code:** indentation is kept exactly as copied, with a configurable tab width, optional line wrapping and optional line numbers.
- **iCloud settings sync:** settings follow you between Macs, and a fresh install restores settings and history automatically.

### Pricing
- Paste Me is free, with no in-app purchases, subscriptions or ads.

### Privacy
- The Privacy Notice now covers settings sync through the iCloud key-value store.

## 1.0 — September 2026 (development build, not released publicly)

- First release: clipboard history with rich previews, syntax-highlighted code, pins and pinboards, "Paste As" transforms, global shortcuts, shelf and list layouts, privacy exclusions and iCloud history sync.
