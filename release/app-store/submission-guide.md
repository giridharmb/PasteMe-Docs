# Mac App Store submission guide

Step by step, from an empty App Store Connect account to "Ready for Sale". Paste Me is free, with no in-app purchases.

The App Store build is sandboxed. It is produced by `scripts/appstore.sh` in the code repository; the normal Xcode build and the DMG are not affected.

## 0. What you need

- Apple Developer Program membership (paid), and your **Team ID** (developer.apple.com ▸ Membership).
- Xcode 16 or later, signed in under Xcode ▸ Settings ▸ Accounts with a role that can upload (Account Holder, Admin or App Manager).
- The bundle ID `com.guy.PasteMe` registered to your team. Xcode registers it during the first archive. If it is already taken by someone else, pick another one and change it in three places: the Xcode target, `PasteMe-AppStore.entitlements` (iCloud container) and `Persistence.cloudKitContainerID`.

### One-time setup in the developer portal

Do these before the first archive. Without them the archive fails with "Your team has no devices from which to generate a provisioning profile" or "Provisioning profile doesn't match the entitlements file's value for the com.apple.developer.icloud-container-identifiers entitlement".

1. **Register your Mac.** Run `system_profiler SPHardwareDataType | grep "Provisioning UDID"`, then add the device at [Devices ▸ +](https://developer.apple.com/account/resources/devices/add) with platform macOS.
2. **Create the iCloud container.** [Identifiers ▸ iCloud Containers ▸ +](https://developer.apple.com/account/resources/identifiers/list/cloudContainer), identifier `iCloud.com.guy.PasteMe`.
3. **Turn on iCloud and push for the app.** [Identifiers](https://developer.apple.com/account/resources/identifiers/list) ▸ `com.guy.PasteMe` ▸ tick **iCloud** (with CloudKit) ▸ Configure ▸ select the container ▸ tick **Push Notifications** ▸ Save.

## 1. Test the sandboxed build locally

```bash
cd ~/git/macosx/"Paste Me"
scripts/appstore.sh sandbox
open "build/appstore/DerivedData/Build/Products/Release/Paste Me.app"
```

This copy is sandboxed but has no iCloud (iCloud needs your team's provisioning profile). Check each item:

- [ ] Settings ▸ Advanced ▸ Pasting Diagnostics says **App Sandbox: on**
- [ ] No Accessibility prompt at any point (the App Store build is compiled with `APP_STORE`)
- [ ] ⇧⌘V, click an item: it is copied and a "Copied — press ⌘V" notice appears; ⌘V pastes it
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

App Store and TestFlight builds use CloudKit's **Production** environment, which starts empty. The schema (record types and their fields) has to be created in **Development** first and then deployed.

CloudKit only creates a record type or a field when a record with a value for it is saved. Using the app by hand therefore leaves gaps: no `CD_Pinboard` until you make a pinboard, and no field for anything that happened to be empty. So let the app create the whole schema:

```bash
scripts/appstore.sh schema --team YOUR_TEAM_ID
```

It builds a development-signed copy with iCloud and runs it once with `-PasteMeInitCloudKitSchema`, which writes one sample record of every type with every field, then removes it. Your history isn't touched. It needs an iCloud account signed in on the Mac.

Then, in the [CloudKit Console](https://icloud.developer.apple.com) ▸ `iCloud.com.guy.PasteMe`:

1. Development ▸ Schema ▸ Record Types: check that `CD_ClipItem`, `CD_ClipRepresentation` and `CD_Pinboard` exist.
2. **Deploy Schema Changes…** ▸ review ▸ Deploy.

If you skip the deploy, sync silently does nothing for App Store and TestFlight users. Repeat both steps whenever the data model changes. A deployed schema can only be added to, never reduced.

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

At least one 16:10 screenshot: 1280×800, 1440×900, 2560×1600 or 2880×1800. Run `scripts/screenshots.sh` in the app repository to generate four from demo data (nothing from your own clipboard), then drag them from `build/screenshots/` into **App Previews and Screenshots**. See the [screenshot notes](../screenshots/README.md).

## 7. App Review information

**Sign-in required:** No.

**Notes** (paste this):

> Paste Me is a clipboard manager. It keeps a history of what the user copies and puts a chosen item back on the clipboard.
>
> How to test:
> 1. Launch the app. A menu bar icon appears and Settings opens.
> 2. Copy some text in any app, then press Shift-Command-V. The history panel opens.
> 3. Click an item (or press Return). It is copied to the clipboard and a "Copied" notice appears. Press Command-V to paste it.
>
> Accessibility: not used. This build doesn't request Accessibility access and doesn't send keystrokes to other apps (Guideline 2.4.5).
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
| Accessibility (Guideline 2.4.5) | Rejected for build 1.2 (4): Apple doesn't accept Accessibility for pressing ⌘V. Since build 6 the App Store build is compiled with `APP_STORE` and doesn't use Accessibility at all; `appstore.sh check` and CI verify the binary. |
| Support URL (Guideline 1.5) | Rejected for build 1.2 (4) because the page only offered GitHub issues. The support page now lists an email address. |
| Name too close to another app (Guideline 4.1) | The store name is "Paste-Me". There is an existing clipboard manager called "Paste", so a reviewer may still ask for a more distinct name. If so, choose one and update `CFBundleDisplayName` and the listing. |
| Store name and app name differ | The store listing says "Paste-Me" and the installed app says "Paste Me". Apple accepts small differences like this; if a reviewer objects, set `CFBundleDisplayName` to "Paste-Me". |
| Launch at login | Off by default; the user turns it on in Settings ▸ General. |
| The app has no window | It is a menu bar app with Settings and a history panel; a Dock icon can be turned on in Settings ▸ General. |

## Differences from the direct-download build

- Data is stored in `~/Library/Containers/com.guy.PasteMe/Data/Library/Application Support/Paste Me/`, so the two builds don't share history unless iCloud sync is on in both.
- The App Store build never pastes for the user and never asks for Accessibility; it copies, and the user presses ⌘V. "Copy selection & pin it" isn't offered.
- Updates are delivered by the App Store.
