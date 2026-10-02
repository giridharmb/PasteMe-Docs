# Export compliance

**Does your app use encryption?** → **No** (only exempt use).

- Paste Me uses SHA-256 (CryptoKit) only to fingerprint clipboard items so duplicates can be detected. Hashing isn't encryption for export purposes.
- Network traffic (link previews, iCloud) uses Apple's system HTTPS/TLS and CloudKit. Using encryption provided by the operating system is exempt.

The app's Info.plist sets `ITSAppUsesNonExemptEncryption` to `false` (in `PasteMe-Info.plist`, merged into the generated Info.plist), so App Store Connect doesn't ask on each upload.

*Not legal advice. Re-evaluate if you add any custom cryptography.*
