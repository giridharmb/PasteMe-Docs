# Release checklist — Paste Me {{VERSION}}

## Code
- [ ] `MARKETING_VERSION` / `CURRENT_PROJECT_VERSION` bumped in the Xcode project
- [ ] `scripts/test.sh all` is green: unit, integration, smoke, performance and end-to-end
- [ ] CI is green on `main`
- [ ] Manual smoke test on a clean macOS 14 account and on the latest macOS:
  - [ ] first launch shows Settings and the Accessibility prompt
  - [ ] ⇧⌘V opens the panel over a full-screen app
  - [ ] paste into TextEdit, Notes, Xcode, Terminal and a browser
  - [ ] image, file, rich text and code items round-trip
  - [ ] password manager copy is skipped
  - [ ] iCloud: turn sync on Mac A, install on Mac B, and history plus settings restore
  - [ ] upgrade from the previous version keeps history

## Build and sign
- [ ] Archive with the **Release** configuration (hardened runtime on)
- [ ] iCloud entitlements (`PasteMe-iCloud.entitlements`) selected for the release build
- [ ] CloudKit schema **deployed to Production** in the CloudKit Console (Development ▸ Deploy Schema Changes)
- [ ] Developer ID build: `TEAM_ID=… scripts/release.sh` → notarized, stapled, `spctl --assess` passes
- [ ] App Store build: uploaded through Xcode Organizer; Transporter validation passes

## Store and docs
- [ ] [metadata.md](app-store/metadata.md) updated: What's New, promo text
- [ ] Screenshots current ([sizes](screenshots/README.md))
- [ ] Price is **Free** in App Store Connect, and no In-App Purchases or subscriptions exist ([pricing](app-store/metadata.md#pricing-and-availability-app-store-connect))
- [ ] No StoreKit in the build: `otool -L "Paste Me.app/Contents/MacOS/Paste Me" | grep -i storekit` prints nothing
- [ ] App Privacy answers still accurate ([app-privacy.md](app-store/app-privacy.md))
- [ ] Privacy Notice / Terms dated and published (GitHub Pages)
- [ ] [CHANGELOG.md](../CHANGELOG.md) and GitHub release notes ([template](release-notes-template.md))
- [ ] Support URL, marketing URL and privacy URL all reachable

## After release
- [ ] Tag `v{{VERSION}}` in the code repository
- [ ] Watch new issues for 48 hours
