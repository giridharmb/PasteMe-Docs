# FAQ

## General

**How do I open my history?**
Press ⇧⌘V, or click the Paste Me icon in the menu bar. You can change the shortcut in Settings ▸ Shortcuts.

**How do I paste something without its formatting?**
Select it and press ⇧↩. You can also press ⌥⇧⌘V anywhere to paste the current clipboard as plain text.

**Why does Paste Me need Accessibility access?**
To press ⌘V in the app you're using. Without it, Paste Me still puts the item on the clipboard and you paste it yourself. [Details](release/accessibility-permission.md).

**Can I find items by the app I copied them from?**
Yes. Use the Apps sidebar in the panel, or ⌥↑ / ⌥↓ to step through apps. ⌘0 shows all apps again and ⌘G shows or hides the sidebar.

## History and storage

**How much history is kept?**
By default, a month of history, up to 1,000 items, within 1 GB in total. When the history gets bigger than that, the oldest items are removed first. Change these limits in Settings ▸ History. Pinned items are never removed automatically.

**Why is the history split into pages?**
To keep the panel fast with very long histories. Choose the page size, or turn pages off, in Settings ▸ History ▸ History Panel.

**Small images have a checkerboard around them. Can I change that?**
Yes. Go to Settings ▸ Appearance ▸ Images and choose checkerboard, transparent, black, white, or any color.

**Can I change the fonts?**
Yes. Settings ▸ Fonts has separate settings for interface text, item titles, preview items, preview text and source code.

**Does code keep its indentation?**
Yes. Tabs expand to tab stops (4 columns by default), lines don't wrap unless you ask them to, and the full preview can show line numbers. Pasting always uses the exact original text.

## iCloud

**What syncs?**
With iCloud sync on: your history, pins and pinboards (through your private CloudKit database). With "Sync settings" on: your layout, fonts, limits, exclusions and shortcuts.

**I set up a new Mac. Do I need to do anything?**
No. Install Paste Me and sign in to the same Apple ID. Paste Me picks up your settings, turns sync back on and downloads your history. If iCloud is slow to deliver your settings, Paste Me offers to restart once they arrive.

**Does sync use my iCloud storage?**
Yes. Images and large items count toward your iCloud storage. Lower the total history size or the largest-item limit to keep this small.

## Privacy

**Does the developer see what I copy?**
No. See the [Privacy Notice](PRIVACY.md).

**Are passwords saved?**
Paste Me skips content that password managers mark as concealed, and excludes common password managers by default.
