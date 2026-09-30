# App Store Connect — App Privacy answers

**Do you or your third-party partners collect data from this app?** → **No, we do not collect data from this app.**

This gives the **"Data Not Collected"** label. The reasons:

| Consideration | Answer |
|---|---|
| Clipboard contents | Stored only on the user's device and in the user's own private iCloud (CloudKit private database and iCloud key-value store). Apple's definition of "collect" means transmitting data off the device in a way that lets **you or your partners** access it for longer than needed to service the request in real time. Private iCloud data isn't accessible to the developer, so it isn't "collected". |
| Link previews | Fetched directly from the linked website by Apple's LinkPresentation framework, on the user's action (copying a link). Nothing is sent to the developer. |
| Analytics / crash reporting | None. If you later add Apple's opt-in crash reports (App Store Connect), they're collected by Apple under the user's consent, not by an SDK in the app. Revisit this page if you add any third-party SDK. |
| Tracking | None. No IDFA, no fingerprinting, no data brokers. |
| Third-party SDKs | None. |

## Privacy manifest

The app bundle includes `PrivacyInfo.xcprivacy`:

- `NSPrivacyTracking`: `false`
- `NSPrivacyCollectedDataTypes`: empty
- Required-reason API: `NSPrivacyAccessedAPICategoryUserDefaults`, reason `CA92.1` (reading and writing the app's own preferences)

## Privacy Policy URL

https://giridharmb.github.io/PasteMe-Docs/PRIVACY
