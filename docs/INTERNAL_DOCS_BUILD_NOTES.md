# Declarative Forms — Docs Build Notes

Internal notes for maintaining and extending this documentation site.

---

## Build date

2026-02-19

## Source files inspected

| File | Key facts extracted |
|------|---------------------|
| `api/src/core/types/form.ts` | Field types (16), validators, connection types, IDeclarativeForm shape |
| `api/src/core/types/submission.ts` | ISubmission shape |
| `api/src/core/services/otp.ts` | OTP constants, token format, flow |
| `api/src/core/services/connections.ts` | Connection handlers, template engine, payload shapes |
| `core/src/components/declarative-form/types.ts` | UI field types (17, includes `rating`), LocaleMap, ICompletion |
| `core/src/components/declarative-form/localized-content.ts` | Locale resolution logic, supported fields |
| `core/src/components/declarative-form/form-helpers.ts` | Navigation resolution, interpolation regex |
| `core/src/components/declarative-form/field-validation.ts` | Validator implementations per field type |
| `core/src/pages/main.page.tsx` | URL structure, prefill, reserved keys, form loading |
| `core/src/pages/thank-you.page.tsx` | Completion page data fetching, template interpolation |
| `.github/profile/README.md` | Feature examples, 48-hour promise, quick start |

---

## Known discrepancies

### `rating` field type
- **Present in:** `core/src/components/declarative-form/types.ts`
- **Absent from:** `api/src/core/types/form.ts`
- **Resolution:** Treat UI types as authoritative for field types. The API type file may be outdated. `rating` is documented as supported.

### Webhook status check
- `handleWebhook` in `connections.ts` does NOT check `submission.status !== 'completed'`
- `handleEmail` and `handleAirtable` DO check `status === 'completed'`
- The docs say "fires on final submission only" — this may be enforced at the caller level (submissions service) rather than in the connection handler
- **Recommendation:** Verify by checking `api/src/core/services/submissions.ts` to confirm when `processConnections` is called
- **Until verified:** Keep documentation as "fires on final submission only" to match expected behavior

### `locale` field
- `locale` is in `core/src/components/declarative-form/types.ts` (UI)
- `locale` is NOT in `api/src/core/types/form.ts`
- The field is used in `main.page.tsx` (`form.locale`)
- Documentation correctly describes this feature; the API type file appears incomplete

---

## Documentation gaps / future additions

1. **Webhook security**: No HMAC signing on outbound webhooks. Worth adding as a feature — would require a `secret` property on the webhook connection.

2. **Email `from` address**: Currently set via server environment variable (`RESEND_FROM_EMAIL`). There's no YAML-level configuration for the sender address. Not documented by design (platform-controlled).

3. **File upload types/extensions**: The `file_upload` field accepts all types. There is no YAML-level filter for accepted MIME types or extensions. If added in future, document it.

4. **Submissions API**: The platform has a submissions API endpoint. It's not documented here because it's not part of the YAML-driven form experience. Add a separate API reference section if/when the API is opened to developers.

5. **Form ID**: The form's `id` is computed server-side from the slug. It's not user-configurable.

6. **`number` field submission value**: Submitted as a string in `data`, not a JavaScript number. Document this in field types (done).

7. **Multiple `when` conditions with same `go`**: Supported — just add multiple rules. No deduplication issue.

8. **`searchable` on `dropdown` vs `multiple_select`**: Both support `searchable: true`. No known differences in behavior.

---

## Navigation structure

The docs use nested groups under "Guides" in `mint.json`. Mintlify supports one level of nesting in the navigation (group → sub-group → pages). The current structure uses this correctly.

---

## Mintlify component usage

Used in docs:
- `<Warning>` — for client-side-only validation notes, JS expression security warnings
- `<Note>` — for informational callouts
- `<CardGroup cols={2}> + <Card>` — for feature grids in introduction
- Standard markdown tables throughout

Not yet used but available:
- `<Tabs>` — could be useful for showing multiple YAML variations
- `<CodeGroup>` — for comparing code snippets
- `<Accordion>` — for FAQ-style content

---

## Maintenance checklist

When updating docs after a code change:

1. Check `core/src/components/declarative-form/types.ts` for new field types
2. Check `api/src/core/services/connections.ts` for new connection types or behavior changes
3. Check `core/src/pages/main.page.tsx` for new reserved query keys
4. Update `INTERNAL_FEATURE_MAP.md` with any new findings
5. Update the changelog
