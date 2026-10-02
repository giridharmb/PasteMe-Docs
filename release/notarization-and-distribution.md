# Distributing outside the Mac App Store (Developer ID)

## One-time setup
1. Join the Apple Developer Program, then create a **Developer ID Application** certificate in Xcode ▸ Settings ▸ Accounts ▸ Manage Certificates.
2. Store notarization credentials in the keychain:
   ```bash
   xcrun notarytool store-credentials PasteMeNotary \
     --apple-id "YOUR_APPLE_ID_EMAIL" --team-id "YOUR_TEAM_ID"
   # notarytool asks for the app-specific password; never put it in a file or a command you save
   ```
3. For iCloud sync in Developer ID builds, enable iCloud (CloudKit + key-value storage) for the App ID `com.guy.PasteMe` in Certificates, Identifiers & Profiles, and create the container `iCloud.com.guy.PasteMe`.

## Each release
Run this from the code repository:

```bash
TEAM_ID=YOUR_TEAM_ID scripts/release.sh PasteMeNotary
```

The script:
1. runs the unit test suite
2. archives the Release configuration (hardened runtime on)
3. exports with `method = developer-id`
4. checks the code signature
5. submits to Apple's notary service and waits
6. staples the ticket and checks it with Gatekeeper (`spctl`)
7. writes `build/release/PasteMe-<version>.zip`

## DMG
`scripts/make-dmg.sh` in the code repository builds a styled drag-to-Applications DMG:
- a Retina background and the app icon as the volume icon
- signed with Developer ID, notarized, stapled and verified
- a SHA-256 checksum file next to it

```bash
scripts/make-dmg.sh --team YOUR_TEAM_ID --notarize PasteMeNotary
# → build/dmg/PasteMe-<version>.dmg (+ .sha256)
```

Without `--team`, it makes an ad-hoc DMG for testing. That DMG includes instructions for opening the app despite Gatekeeper.

## Verify on a clean Mac
```bash
spctl --assess --type execute --verbose "/Applications/Paste Me.app"   # accepted, source=Notarized Developer ID
codesign -dv --verbose=4 "/Applications/Paste Me.app"                    # Runtime flag present, TeamIdentifier set
```

## Updates
Paste Me doesn't include an auto-updater. Options:
- publish new builds on GitHub Releases and announce them in the changelog
- add Sparkle 2, which needs an EdDSA key and an appcast
