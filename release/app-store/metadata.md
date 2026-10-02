# Mac App Store listing

| Field | Value | Limit |
|---|---|---|
| **Name** | Paste Me — Clipboard Manager | 30 |
| **Subtitle** | Searchable clipboard history | 30 |
| **Primary category** | Productivity | |
| **Secondary category** | Developer Tools | |
| **Price** | Free (USD 0.00, all territories) | |
| **In-App Purchases** | None | |
| **Subscriptions** | None | |
| **Ads / tracking** | None | |
| **Support URL** | https://giridharmb.github.io/PasteMe-Docs/SUPPORT | |
| **Marketing URL** | https://giridharmb.github.io/PasteMe-Docs/ | |
| **Privacy Policy URL** | https://giridharmb.github.io/PasteMe-Docs/PRIVACY | |
| **Copyright** | © 2026 Giridhar Bhujanga (must match `NSHumanReadableCopyright` in the app) | |
| **SKU** | PASTEME-MAC-001 | |
| **Bundle ID** | com.guy.PasteMe | |

## Pricing and availability (App Store Connect)

Paste Me is free. It has no in-app purchases, subscriptions, ads, trials or paid tiers.

- **Pricing and Availability ▸ Price Schedule:** set the base price to **Free (USD 0.00)** for every country or region. Don't schedule any future price change.
- **Monetization ▸ In-App Purchases / Subscriptions:** leave empty. Don't create products or subscription groups.
- **Agreements:** only the Free Apps agreement is needed. You don't have to sign the Paid Apps agreement or add banking or tax information for Paste Me.
- **App Privacy:** "Data Not Collected" stays accurate: there are no ads, no purchases and no analytics ([app-privacy.md](app-privacy.md)).
- **Code:** the app doesn't link StoreKit and has no In-App Purchase capability. Keep it that way. The release checklist verifies this.

## Promotional text (170)

Everything you copy, one keystroke away. Search, pin and paste text, code, links and images with their formatting intact — privately, on your Mac.

## Description (4000)

Paste Me remembers everything you copy so you never lose a snippet again. Press ⇧⌘V anywhere to open your clipboard history. Type to search, then press Return to paste into the app you're using, with the original formatting.

EVERYTHING YOU COPY
• Text, rich text, source code, links, images, files, colors and email addresses
• Every format is kept, so RTF, HTML and images paste back exactly as copied
• Paste as plain text with Shift-Return

MADE FOR DEVELOPERS
• Detects 20+ languages and highlights them with 8 themes
• Indentation preserved exactly, with tab width, wrapping and line numbers
• Paste code as highlighted rich text into Notes, Mail and Keynote
• "Paste As": camelCase, snake_case, pretty or minified JSON, Base64, URL encoding, Markdown and more

FIND IT FAST
• Instant search across your whole history
• Apps sidebar: browse clips by the app you copied from, with Option-arrow keys
• Filter by type: images, links, code, files, colors
• Full keyboard control, Quick Look preview and ⌘1–⌘9 quick paste
• Quick Paste: ⌃⌥V then 0–9 pastes one of ten favorite snippets in any app

ORGANIZE
• Pin favorite snippets and group them into color-coded pinboards
• Rename items, drag them into other apps

FREE, WITH NOTHING TO BUY
• No in-app purchases, no subscriptions, no ads

PRIVATE BY DESIGN
• No accounts, no analytics, no tracking
• Skips passwords from password managers automatically
• Exclude any app, pause capture, clear history on quit
• Optional iCloud sync through your own private iCloud

YOURS TO TUNE
• Shelf or list layout, light or dark, custom fonts
• History limits: retention, item count, page size, total size
• Customizable global shortcuts, with a master switch and apps that keep their own keys
• Start at login

Paste Me needs Accessibility permission only to press ⌘V for you. Without it, items are still copied to your clipboard.

## Keywords (100)

clipboard,history,paste,copy,snippets,manager,pasteboard,developer,code,pin,text,productivity

## What's New (4000)

See the [Changelog](../../CHANGELOG.md). Paste the current version's entries here.

## App Review notes

> Paste Me is a clipboard manager. To review it:
> 1. Launch the app. A menu bar icon appears and Settings opens.
> 2. Copy some text in any app, then press ⇧⌘V to open the history panel.
> 3. Press Return to paste. This needs **Accessibility** permission (System Settings ▸ Privacy & Security ▸ Accessibility). Paste Me uses it only to send ⌘V/⌘C to the frontmost app. Without the permission, the chosen item is copied to the clipboard instead.
>
> No account or login is required. iCloud sync is optional (Settings ▸ iCloud).

> App Sandbox is enabled in the App Store build. Pasting sends ⌘V with CGEvent, which macOS allows after the user turns on Accessibility. The full review note, with the list of entitlements, is in the [submission guide](submission-guide.md#7-app-review-information).
