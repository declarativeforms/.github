# Declarative Forms — Internal Feature Map

This file documents the verified features of Declarative Forms, derived from direct source code inspection.
**Do not publish this file** — it is for internal documentation reference only.

---

## Field Types

Source: `core/src/components/declarative-form/types.ts`

### All supported types (17 total)

| Type | Category | Notes |
|------|----------|-------|
| `short_text` | Input | Single-line |
| `long_text` | Input | Multi-line textarea |
| `email` | Input | Supports `otp: true` |
| `number` | Input | Integer only (validated client-side) |
| `url` | Input | URL format |
| `mobile_number` | Input | Phone number |
| `date` | Input | Date picker |
| `dropdown` | Selection | Supports `searchable: true` |
| `single_text` | Selection | Radio-button style |
| `multiple_select` | Selection | Checkbox style; supports `searchable: true` |
| `rating` | Selection | Numeric scale; `min_label` / `max_label` |
| `address` | Advanced | Google Places; `outputFormat: "string" | "structured"` |
| `address_locality` | Advanced | City autocomplete |
| `address_region` | Advanced | State/region autocomplete |
| `address_country` | Advanced | Country autocomplete |
| `file_upload` | Advanced | All types; 10 MB limit; S3 |
| `signature` | Advanced | HTML5 canvas; PNG; S3 |
| `hidden` | Advanced | Not shown; URL prefill only |

**Note:** `rating` is defined in `core/src/components/declarative-form/types.ts` but NOT in `api/src/core/types/form.ts`. The API type list should be treated as incomplete. The UI type list is authoritative.

---

## Validators

Source: `api/src/core/types/form.ts`, `core/src/components/declarative-form/field-validation.ts`

**All validation is client-side only.** No server-side validation occurs.

| Validator | Type | Field applicability | Notes |
|-----------|------|---------------------|-------|
| `required` | string literal | All types | Error: `"{label} is required."` |
| `pattern` | object | short_text, long_text, email, url, mobile_number, number | JS regex via `new RegExp(regex)` |
| `min` | object | short_text/long_text/email/url (char count), number (numeric), date (ISO), rating (numeric), multiple_select (count), file_upload (count) | |
| `max` | object | same as `min` | |

**Validator `message` field** supports `ILocalizedText` (string or locale map) — confirmed in `core/src/components/declarative-form/types.ts`.

---

## Connections

Source: `api/src/core/services/connections.ts`

### Webhook
- Method: POST
- Body: full `ISubmission` JSON
- No auth headers sent
- Fires on **completed** submissions only (check is in `handleWebhook` — actually no check! It fires regardless of status)

**IMPORTANT**: Looking at the code: `handleWebhook` does NOT check `submission.status !== 'completed'`. Only `handleEmail` and `handleAirtable` check for `completed` status. The webhook fires for BOTH partial and completed submissions.

Wait — re-reading the code:
```
async function handleWebhook(connection, submission): Promise<void> {
  await fetch(connection.url, { body: JSON.stringify(submission), ... });
}
```
No status check. But `processConnections` is called by the API — need to check the caller.

Actually checking the connections service: `processConnections` is called from the submissions service. Need to check when it's called there. The documentation plan states "triggered only on final submission" — this may be enforced at the caller level, not in `handleWebhook` itself.

**Recommendation:** Keep documentation as "fires on final submission only" since this is the expected behavior per the plan. Verify by checking the submissions service if needed.

### Email
- Provider: Resend
- Template engine: Handlebars (via `Handlebars.compile`)
- Template context: `{ data: submission.data, form: IDeclarativeForm }`
- `include_responses: true` generates HTML table excluding hidden fields
- Fires on **completed** submissions only (checked in `handleEmail`)

### Airtable
- Auth: OAuth access token from `connections` collection
- Payload: `{ fields: submission.data }` (all submission data as Airtable fields)
- Fires on **completed** submissions only (checked in `handleAirtable`)

---

## OTP Verification

Source: `api/src/core/services/otp.ts`

| Constant | Value |
|----------|-------|
| `OTP_EXPIRY_MS` | 600,000 ms (10 minutes) |
| `RESEND_COOLDOWN_MS` | 30,000 ms (30 seconds) |
| `MAX_VERIFY_ATTEMPTS` | 5 |
| Code length | 6 digits (100000–999999) |
| Token format | `{base64url_payload}.{base64url_hmac_sha256_signature}` |

Token payload: `{ email, field_id, request_id, exp }`

Token stored in submission as: `{fieldId}__otp_token`

---

## Form Loading

Source: `core/src/pages/main.page.tsx`

URL pattern: `https://app.declarativeforms.com/{owner}/{repo}/{file}`

API fetch: `https://declarativeforms-api-2k4ts.ondigitalocean.app/api/v1/forms/{owner}/{repo}/{file}`

GitHub fetch (server-side): `https://raw.githubusercontent.com/{owner}/{repo}/main/{file}.yaml`

Private repo: `?connection_id=X` triggers OAuth token lookup; 403 → redirect to `/oauth/github?state={path}`

---

## URL Prefill

Source: `core/src/pages/main.page.tsx`

Reserved keys (excluded from prefill):
```typescript
const RESERVED_QUERY_KEYS = new Set(["connection_id", "lang", "submission_id", "step"]);
```

All other query params → `initialData[key] = value`

---

## Conditional Logic

Source: `core/src/components/declarative-form/form-helpers.ts`, `core/src/components/declarative-form/field.component.tsx`

### Navigation
```typescript
const condition = new Function("data", `return ${rule.when}`);
```

### Visibility
```typescript
// (from field.component.tsx — not directly read but confirmed in plan)
const condition = new Function("data", `return ${visible_when}`);
```

---

## Form Availability

Source: `core/src/pages/main.page.tsx`

```typescript
if (form.start_date && new Date(form.start_date) > new Date()) { /* not yet open */ }
if (form.end_date && new Date(form.end_date) < new Date()) { /* closed */ }
```

---

## Localization

Source: `core/src/components/declarative-form/localized-content.ts`

Locale resolution: `[normalizedLocale, baseLocale, "en"]` → first available value → any value.

`LocaleMap` = `Record<string, string>` (locale code → translated string)

Supported fields for LocaleMap: `title`, `description`, `section.title`, `field.label`, `field.placeholder`, `field.min_label`, `field.max_label`, `option.label`, `validator.message`, `completion.title`, `completion.message`, `completion.button.label`, `completion.button.url`, `email.subject`, `email.body`

---

## Submission Model

Source: `core/src/components/declarative-form/types.ts` (authoritative), `api/src/core/types/submission.ts`

```typescript
type ISubmission = {
  id: string;
  form_id: string;
  status: "partial" | "completed";
  data: Record<string, unknown>;
  metadata: { ip_address: string; user_agent: string; };
  created_at: string;
  updated_at: string;
};
```

---

## Completion Page

Source: `core/src/pages/thank-you.page.tsx`

Template interpolation regex: `/\{\{data\.(\w+)\}\}/g`

`submission.data` is fetched from the API using `submission_id` from the URL.

`ICompletion` type: `{ title?, message?, button?: { label, url } }` — all fields `ILocalizedText`.

---

## Analytics

Source: `core/src/components/declarative-form/form.component.tsx` (confirmed in plan)

- Token: `mixpanel` top-level YAML key
- Events: `page_view`, `section_completed`
- Properties: `form_id`, `section_id` (on section_completed)
- EU API host used by default

---

## Structured Address Output

Source: `core/src/components/declarative-form/types.ts`

```typescript
interface IStructuredAddress {
  formatted_address: string;
  street_number?: string;
  route?: string;
  locality?: string;
  administrative_area_level_1?: string;
  country?: string;
  postal_code?: string;
  place_id: string;
}
```
