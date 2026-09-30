# Paste Me Privacy Notice

**Effective date:** {{EFFECTIVE_DATE}} · **Applies to:** Paste Me for macOS, version 1.1 and later

Paste Me is a clipboard manager. Its whole job is to remember what you copy, so this notice explains exactly what it stores, where, and who can see it.

**The short version:** your clipboard history stays on your Mac, plus your own private iCloud if you turn on sync. The developer never receives it. Paste Me contains no analytics, advertising or tracking code, and it has no accounts.

## 1. What Paste Me stores

| Data | Why | Where |
|---|---|---|
| Items you copy: text, rich text, code, links, images, file references, colors | To show your history and paste items back | On your Mac: `~/Library/Application Support/Paste Me/` |
| Details about each item: time copied, source app name and bundle ID, size, detected type/language, your pins, titles and pinboards | Search, grouping by app, sorting, retention | Same place |
| Link titles and icons (optional) | To show readable link previews | Same place |
| Your settings | To remember your preferences | macOS preferences (`com.guy.PasteMe`) |

File items store the file's location (a file URL), not a copy of the file.

### What Paste Me never stores

- **Content from password managers and other apps that mark clipboard data as concealed or transient** ([nspasteboard.org](http://nspasteboard.org) conventions). This is on by default.
- **Anything copied while an excluded app is in front.** 1Password, Bitwarden, LastPass, Dashlane, KeePassXC, Keychain Access and Passwords are excluded by default. You can add any app.
- **Anything copied while capture is paused.**

## 2. What leaves your Mac

**Nothing is sent to the developer.** Paste Me has no servers, analytics, crash reporting SDK or advertising identifiers.

Data leaves your Mac only in these cases:

1. **iCloud sync (off by default).** When you turn it on, your history syncs through **your private iCloud database** (Apple CloudKit), and your settings sync through the iCloud key-value store. This data sits in your iCloud account under Apple's [iCloud terms](https://www.apple.com/legal/internet-services/icloud/) and [privacy policy](https://www.apple.com/legal/privacy/). The developer cannot access your private iCloud database. Turn sync off at any time in Settings ▸ iCloud.
2. **Link previews (on by default).** When you copy a web link, Paste Me uses Apple's LinkPresentation framework to fetch that page's title and icon. The website sees a normal request from your Mac, including your IP address, just as if you'd opened the link. To turn this off, go to Settings ▸ History ▸ "Fetch titles and icons for links".
3. **Things you do on purpose.** Pasting into another app, dragging an item out, opening a link or exporting your history to a file.

## 3. Permissions

- **Accessibility.** Used only to send ⌘V (paste) and, for the optional "Copy selection & pin it" shortcut, ⌘C to the app you're using. Paste Me does not read your screen or record your keystrokes. Without this permission, Paste Me still copies items to the clipboard for you to paste manually. [More details](release/accessibility-permission.md).
- **Clipboard.** macOS lets apps read the clipboard. Paste Me checks it for changes several times a second while capture is on, and only while the app is running.
- **Launch at login (optional).** Managed through macOS Login Items.

## 4. How long data is kept

You decide. Settings ▸ History has these limits:

- **Retention period:** 1 day to forever. The default is 1 month.
- **Maximum number of items:** the default is 1,000.
- **Total history size:** the default is 1 GB. The oldest items are removed first.

Pinned items and pinboards are kept until you delete them. You can also clear your history, delete everything, or have history cleared every time you quit (Settings ▸ Privacy).

## 5. Your choices and controls

- **Delete items:** delete any item (⌘⌫), clear your history, or delete everything (Settings ▸ History).
- **Export or import:** export your history or pinned items as a JSON file you control (Settings ▸ Advanced).
- **iCloud data:** turn off iCloud sync and delete the data Paste Me stored there under System Settings ▸ Apple ID ▸ iCloud ▸ Manage.
- **Remove all local data:** quit Paste Me and delete `~/Library/Application Support/Paste Me/`.

## 6. Children

Paste Me is a general-purpose utility. It does not knowingly collect personal information from anyone, including children, because it doesn't send data to the developer at all.

## 7. Security

Your history is stored in your macOS user account and protected by macOS file permissions and FileVault if you use it. iCloud data is protected by Apple's iCloud security, and by end-to-end encryption if you turn on Advanced Data Protection. [How to report a security issue](SECURITY.md).

## 8. Changes to this notice

If this notice changes, the new version and date are published in this repository. Material changes are also called out in the [Changelog](CHANGELOG.md).

## 9. Contact

{{DEVELOPER_NAME}} · {{CONTACT_EMAIL}} · or open an issue at <https://github.com/giridharmb/PasteMe-Docs/issues>.
