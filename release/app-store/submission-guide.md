# Mac App Store submission guide

Step by step, from an empty App Store Connect account to "Ready for Sale". Paste Me is free, with no in-app purchases.

The App Store build is sandboxed. It is produced by `scripts/appstore.sh` in the code repository; the normal Xcode build and the DMG are not affected.

## 0. What you need

- Apple Developer Program membership (paid), and your **Team ID** (developer.apple.com ▸ Membership).
- Xcode 16 or later, signed in under Xcode ▸ Settings ▸ Accounts with a role that can upload (Account Holder, Admin or App Manager).
- The bundle ID `com.guy.PasteMe` registered to your team. Xcode registers it during the first archive. If it is already taken by someone else, pick another one and change it in three places: the Xcode target, `PasteMe-AppStore.entitlements` (iCloud container) and `Persistence.cloudKitContainerID`.

## 1. Test the sandboxed build locally

```bash
cd ~/git/macosx/"Paste Me"
scripts/appstore.sh sandbox
open "build/appstore/DerivedData/Build/Products/Release/Paste Me.app"
```

This copy is sandboxed but has no iCloud (iCloud needs your team's provisioning profile). Check each item:

- [ ] Settings ▸ Advanced ▸ Pasting Diagnostics says **App Sandbox: on**
- [ ] Accessibility: turn it on for this copy, then **Test Paste in 3 Seconds** pastes into TextEdit
- [ ] ⇧⌘V, click an item: it pastes into the app you were using
- [ ] Quick Paste: ⌃⌥V then a digit
- [ ] Copy a file in Finder, quit and reopen Paste Me, paste the file from history into Finder and into Mail
- [ ] A copied link gets its title and icon (network access)
- [ ] Settings ▸ Advanced ▸ Export, then Import
- [ ] Settings ▸ Privacy ▸ Add App…
- [ ] Start at login on, log out and in

## 2. Create the app record

In [App Store Connect](https://appstoreconnect.apple.com) ▸ Apps ▸ **+** ▸ New App:

| Field | Value |
|---|---|
| Platform | macOS |
| Name | Paste-Me ("Paste Me" was already taken on the store) |
| Primary language | English (U.S.) |
| Bundle ID | com.guy.PasteMe |
| SKU | PASTEME-MAC-001 |
| User access | Full access |

Then fill in the listing from [metadata.md](metadata.md): subtitle, promotional text, description, keywords, support URL, marketing URL, privacy policy URL, copyright.

- **Pricing and Availability:** Free, all territories. See [metadata.md](metadata.md#pricing-and-availability-app-store-connect).
- **App Privacy:** answer "Data Not Collected". See [app-privacy.md](app-privacy.md).
- **Age rating:** see [age-rating.md](age-rating.md).
- **Category:** Productivity (secondary: Developer Tools).

The support, marketing and privacy URLs must be live before you submit. Publish this repository with GitHub Pages first: Settings ▸ Pages ▸ Deploy from a branch ▸ `main`, `/ (root)`.

## 3. iCloud (CloudKit)

1. The first archive with your team creates the container `iCloud.com.guy.PasteMe`.
2. Run the archived app once from Xcode's Organizer, or a development build with `PasteMe-AppStore.entitlements`, with iCloud sync on. Copy a few things. This creates the record types in the **Development** environment.
3. In the [CloudKit Console](https://icloud.developer.apple.com) ▸ your container ▸ Schema ▸ **Deploy Schema Changes…** to Production.

If you skip step 3, sync silently does nothing for App Store users.

## 4. Upload a build

Each upload needs a build number that App Store Connect hasn't seen for this version.

```bash
scripts/appstore.sh upload --team YOUR_TEAM_ID --build 4
```

The script runs the unit tests, archives with the sandboxed entitlements, verifies the result (sandbox on, entitlements, universal binary, Info.plist, privacy manifest, no StoreKit) and uploads. The build shows up under TestFlight after 5 to 30 minutes.

To upload by hand instead: `scripts/appstore.sh archive --team YOUR_TEAM_ID --build 4`, then drag `build/appstore/export/Paste Me.pkg` into the **Transporter** app.

## 5. TestFlight (recommended)

Install the processed build through TestFlight on a second Mac, or a second user account, and repeat the checklist from step 1. Also check iCloud sync between two Macs, and a fresh install restoring history.

## 6. Screenshots

At least one 16:10 screenshot: 1280×800, 1440×900, 2560×1600 or 2880×1800. See the [shot list](../screenshots/README.md).

## 7. App Review information

**Sign-in required:** No.

**Notes** (paste this):

> Paste Me is a clipboard manager. It keeps a history of what the user copies and pastes a chosen item back into the app they are using.
>
> How to test:
> 1. Launch the app. A menu bar icon appears and Settings opens.
> 2. Copy some text in any app, then press Shift-Command-V. The history panel opens.
> 3. Click an item (or press Return) to paste it into the frontmost app.
>
> Accessibility permission: pasting works by sending the Command-V keystroke to the frontmost app with CGEvent, which macOS only allows after the user turns on Paste Me under System Settings > Privacy & Security > Accessibility. The app asks for this the first time the user pastes and explains why. Without the permission the chosen item is still copied to the clipboard and the app tells the user to press Command-V. The app does not read the screen, does not record keystrokes and does not use the Accessibility API to inspect other apps.
>
> Global shortcuts are registered with RegisterEventHotKey and react only to the combinations the user sets.
>
> App Sandbox is enabled. Entitlements: outgoing network connections (link titles and icons through LinkPresentation, and iCloud), user-selected file access (Export/Import and choosing apps to exclude), app-scoped bookmarks (to paste a copied file again after the app restarts), and iCloud (CloudKit private database and key-value store for optional sync).
>
> The app is free. It has no accounts, no purchases, no ads and no analytics. Clipboard data stays on the user's Mac and, if they turn on sync, in their private iCloud database.

**Contact information:** your name, phone and email. Apple uses these only to reach you during review; they are not shown on the store.

## 8. Submit

Select the build under the macOS version, answer the export-compliance question if asked (the app declares no non-exempt encryption, see [export-compliance.md](export-compliance.md)), then **Add for Review** ▸ **Submit**.

## Things App Review may raise

| Topic | Answer |
|---|---|
| "Why does the app need Accessibility?" (Guideline 2.4.5) | Use the note above: only to send ⌘V; the app works in copy-only mode without it. |
| Name too close to another app (Guideline 4.1) | The store name is "Paste-Me". There is an existing clipboard manager called "Paste", so a reviewer may still ask for a more distinct name. If so, choose one and update `CFBundleDisplayName` and the listing. |
| Store name and app name differ | The store listing says "Paste-Me" and the installed app says "Paste Me". Apple accepts small differences like this; if a reviewer objects, set `CFBundleDisplayName` to "Paste-Me". |
| Launch at login | Off by default; the user turns it on in Settings ▸ General. |
| The app has no window | It is a menu bar app with Settings and a history panel; a Dock icon can be turned on in Settings ▸ General. |

## Differences from the direct-download build

- Data is stored in `~/Library/Containers/com.guy.PasteMe/Data/Library/Application Support/Paste Me/`, so the two builds don't share history unless iCloud sync is on in both.
- Accessibility has to be granted to the App Store copy separately.
- Updates are delivered by the App Store.
