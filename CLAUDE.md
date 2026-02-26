# Declarative Forms — Guide Authoring Rules

## Guide Structure

Every guide must follow this exact skeleton:

```
---
title: "Build a [Use Case] Form" or "Build a [Use Case] Form with [Capability]"
description: One sentence — what the reader will build.
---

Outcome statement (1-2 sentences: what you'll build + what capability you'll learn)

---

## Define the form

Full YAML in a single fenced code block. Filename instruction above it.

---

## Deploy it

git add/commit/push + URL pattern. Identical across all guides.
```

## Guide Roster

| # | Title | Use Case | Capability Introduced | Key Concepts |
|---|-------|----------|----------------------|--------------|
| 1 | Build a Newsletter Signup Form | Newsletter signup | Form basics | `version`, `title`, `description`, `sections`, `fields`, `validators`, `next` |
| 2 | Build an Event RSVP Form with Conditional Logic | Event registration | Conditional branching | `next` with `when`/`go`/`else`, multi-section |
| 3 | Build a Feedback Form with Email Notification | Feedback collection | Email connection | `connections`, `type: email`, Handlebars templating |
| 4 | Build a Job Application Form with File Uploads | Job application | File uploads | `type: file_upload`, `type: mobile_number`, `max` validator |
| 5 | Build a Customer Survey Form with Ratings | Customer survey | Rating field | `type: rating`, `min_label`, `max_label` |
| 6 | Build a Contact Form with Webhook Integration | Contact form | Webhook connection | `connections`, `type: webhook` |
| 7 | Build a Registration Form with Email Verification | Registration | OTP verification | `otp: true` on email fields, `type: email` |
| 8 | Build a Booking Form in Multiple Languages | Booking | Localization | `locale`, `ILocalizedText`, `?lang=` |
| 9 | Build an Order Form with Conditional Fields | Order form | Conditional field visibility | `visible_when` |
| 10 | Build a Waitlist Signup Form with a Custom Completion Screen | Waitlist signup | Completion screen | `completion`, `title`, `message`, `button`, `{{data.fieldId}}` |
| 11 | Build a Country Selector Form with a Searchable Dropdown | Country selector | Searchable dropdown | `type: dropdown`, `searchable: true` |
| 12 | Build a Referral Form with URL Prefill | Referral form | URL prefill | Query parameters as initial field values, reserved params (`connection_id`, `lang`, `submission_id`, `step`) |
| 13 | Build an Invite Form with Pattern Validation | Invite-only signup | Pattern validator | `type: pattern`, `regex`, `message` |
| 14 | Build an Interest Survey Form with Multiple Selection | Interest survey | Multiple select field | `type: multiple_select`, `options`, array submission |
| 15 | Build a Donation Form with a Number Field | Donation form | Number field | `type: number`, whole-number validation, numeric keyboard |
| 16 | Build a Lead Capture Form with a Hidden Field | Lead capture | Hidden field | `type: hidden`, no visible UI, value from URL query params |
| 17 | Build a Volunteer Signup Form with Address Autocomplete | Volunteer signup | Address field | `type: address`, Google Places autocomplete |
| 18 | Build a Consent Form with a Signature Field | Photo release consent | Signature field | `type: signature`, canvas drawing, auto-upload PNG |
| 19 | Build a Contest Entry Form with Scheduling | Contest entry | Scheduling | `start_date`, `end_date`, date-based form availability |
| 20 | Build a Review Form with Minimum Length Validation | Product review | Min validator | `type: min`, `value`, `message`, character count enforcement on text fields |
| 19 | Build a Workshop Registration Form with Airtable Integration | Workshop registration | Airtable connection | `connections`, `type: airtable`, `connection_id`, `base_id`, `table_id_or_name` |

## Authoring Rules

- **Title pattern**: "Build a [Use Case] Form" (guide 1) or "Build a [Use Case] Form with [Capability]" (guides 2+)
- **One capability per guide**: each guide introduces exactly ONE new capability
- **Complete YAML**: the YAML example must be a complete, valid form — never a fragment
- **Semantic IDs**: use `signup`, `name`, `email` — never `section_1` / `question_1`
- **"Deploy it" is identical**: copy-paste the same deploy section across all guides
- **Pure Markdown**: no Mintlify components — use `---` separators between sections

## Reference Page Rules

- **Location**: `docs/reference/`
- **Title**: `Form`, `Section` for structural pages; exact type name for fields (`short_text`, `email`, `dropdown`)
- **Description**: one sentence
- **Content**: a single fenced YAML code block with inline `#` comments — no prose, no headings below frontmatter
- **Comment style**: `# Required.` or `# Optional.` first, then type/default, then behavior notes
- **Property order**: `id` → `type` → `label` → `placeholder` → type-specific props → `visible_when` → `validators`
- **Validator order**: `required` → `min` → `max` → `pattern`
- **Commented-out lines**: show alternative syntax or optional properties
- **No Mintlify components**: pure Markdown only

## Concept Page Rules

- **Location**: `docs/concepts/`
- **Title**: the concept name (`Form`, `Sections`, `Fields`, `Connections`, `Localization`, `Analytics`)
- **Description**: one sentence
- **Voice**: second person ("you"), present tense, direct and confident
- **Tone**: clear, calm, and purposeful — no hype, no hedging
- **Density**: one idea per paragraph, short sentences, no filler
- **Structure**: core/required properties first, then optional properties ordered by importance
- **YAML snippets**: short and focused — show only the properties being discussed, not full forms
- **Cross-references**: mention other concept pages by name with links, but never re-explain their content
- **No bleed**: each page owns exactly its scope — Form doesn't explain sections, Fields doesn't cover connections
- **Separators**: use `---` between major sections
- **No Mintlify components**: pure Markdown only
