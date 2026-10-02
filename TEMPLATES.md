# Templates

The documents in this repository are filled in. Only the per-release templates still contain `{{PLACEHOLDER}}` values, which you replace each time you ship:

| File | Placeholders |
|---|---|
| [release/release-notes-template.md](release/release-notes-template.md) | `{{VERSION}}`, `{{ONE_LINE_SUMMARY}}`, `{{FEATURE}}`, `{{IMPROVEMENT}}`, `{{FIX}}`, `{{DOWNLOAD_LINK}}` |
| [release/release-checklist.md](release/release-checklist.md) | `{{VERSION}}` |

To list what's left:

```bash
grep -rn "{{" --include=*.md .
```

## If you fork these documents

Change these to your own details:

- the developer name in [README.md](README.md), [PRIVACY.md](PRIVACY.md), [TERMS.md](TERMS.md) and the copyright line in [release/app-store/metadata.md](release/app-store/metadata.md)
- the effective dates in [PRIVACY.md](PRIVACY.md) and [TERMS.md](TERMS.md)
- the contact links (GitHub issues) in [SUPPORT.md](SUPPORT.md), [SECURITY.md](SECURITY.md), [TERMS.md](TERMS.md), [PRIVACY.md](PRIVACY.md) and [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md)

Never commit real passwords, app-specific passwords or API keys.
