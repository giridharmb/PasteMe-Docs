# Filling in the templates

Search for `{{` and replace each placeholder:

| Placeholder | Example |
|---|---|
| `{{DEVELOPER_NAME}}` | Your legal or trading name |
| `{{CONTACT_EMAIL}}`, `{{SECURITY_EMAIL}}` | support@example.com |
| `{{EFFECTIVE_DATE}}`, `{{RELEASE_DATE}}`, `{{RELEASE_DATE_1_0}}`, `{{YEAR}}` | 2026-10-01 |
| `{{RESPONSE_TIME}}`, `{{ACK_TIME}}` | 2 business days |
| `{{TEAM_ID}}`, `{{APPLE_ID}}`, `{{APP_SPECIFIC_PASSWORD}}` | App Store / developer account values (never commit real passwords) |
| `{{VERSION}}`, `{{ONE_LINE_SUMMARY}}`, `{{FEATURE}}`, … | Per release |

```bash
grep -rn "{{" --include=*.md .
```
