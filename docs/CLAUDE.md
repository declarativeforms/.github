# Declarative Forms — Docs Authoring Guide

Read this file before adding or editing any page in this docs site.

---

## Audience

Engineers and technical builders. Comfortable with YAML, git, and CLI. May be using LLM coding tools (Claude Code, Codex) to generate forms. Write as if the reader is a competent developer, not a beginner. Skip the hand-holding; don't skip the precision.

---

## Source of truth for types

Before documenting any behavior, verify it against the source:

- **Field types and shapes:** `core/src/components/declarative-form/types.ts`
- **Connection implementation:** `api/src/core/services/connections.ts`
- **Validators:** `core/src/components/declarative-form/field-validation.ts`

The API types file (`api/src/core/types/form.ts`) is incomplete — do not use it as the sole source.

---

## Navigation structure

```
Getting Started: introduction, quickstart, how-it-works
Guides: add-steps, conditional-fields, conditional-navigation, notify-team, webhook, airtable, localization, analytics
Reference: yaml-schema, short-text, long-text, multiple-select, single-select, dropdown
Help: support
```

- New field type → add to Reference group
- New platform feature → add to Guides group
- All pages must be listed in `mint.json` navigation

---

## Tone and style

- Prose-first. Explain with sentences before tables.
- Short sentences. Active voice. No filler.
- No CardGroup, no Tabs, no Step components unless absolutely necessary. Use plain headings + prose + code blocks + tables.
- Code blocks: always use `yaml` or `json` syntax highlighting.
- No emojis.

---

## Quickstart canonical form

`rental.yaml` — the rental application form — is the canonical example throughout the docs:

```yaml
version: 1
title: Rental Application
sections:
  - id: main
    title: Apply to rent
    fields:
      - id: full_name
        type: short_text
        label: Full name
        validators:
          - required
      - id: email
        type: email
        label: Email address
        validators:
          - required
      - id: move_in_date
        type: date
        label: Desired move-in date
        validators:
          - required
    next: done
```

- File name: `rental.yaml`
- URL pattern: `https://app.declarativeforms.com/{owner}/{repo}/rental`
- Field IDs: `full_name`, `email`, `move_in_date`

Do not change the field IDs or field types in this form without updating all pages that reference it.

---

## Field reference page template

Every field type page must follow this structure:

1. **Frontmatter:** `title: {type}`, `description: one sentence`
2. **Opening:** what the field renders as; submission value type (`string`, `string[]`, etc.)
3. **Properties table:** all properties applicable to this type
4. **Validators section:** one subsection per applicable validator. Each subsection has: description, YAML snippet, properties table (if applicable), default error message
5. **`<Warning>` callout:** "Validators run in the browser before each section is submitted. They enforce UX constraints, not security guarantees. If you need server-side validation, implement it in your webhook receiver."
6. **Full example:** complete field definition using realistic values

---

## Guide page template

Every Guides page must follow this structure:

1. **Frontmatter:** `title:`, `description:`
2. **Opening paragraph:** what feature this page adds and why it matters
3. **What to add:** show the YAML diff/addition (not a full rewrite of unchanged sections)
4. **Explanation:** cover key properties, behavior, and edge cases
5. **Complete working form:** the full `rental.yaml` as it stands after adding this feature
6. **Cross-links** at the end to related pages

---

## Localization coverage

Every page that covers a property supporting LocaleMap must show both the plain-string and locale-map syntax. Don't just mention it — show it.

---

## Internal links

Only link to pages that exist in `mint.json` navigation. When in doubt, check `mint.json`.

---

## Adding a new field type reference page

1. Copy the structure from an existing reference page (e.g., `short-text.mdx`)
2. Check `types.ts` for all applicable properties
3. Check `field-validation.ts` for validator behavior specific to this type (`min`/`max` semantics differ by type)
4. Add the page to the `reference` group in `mint.json`
5. Update `reference/yaml-schema.mdx` to link to the new page in the field types table

---

## Consistency standards

| Concern | Standard |
|---------|----------|
| Quickstart form file | `rental.yaml` |
| Form URL pattern | `https://app.declarativeforms.com/{owner}/{repo}/rental` |
| Field IDs in quickstart form | `full_name`, `email`, `move_in_date` |
| LocaleMap format | `{en: "...", es: "..."}` — always show both |
| Validator warning | Always use `<Warning>` callout, always client-side-only |
| Connections: when they fire | "fire once when `status` becomes `completed`" |
| Airtable OAuth path | `https://app.declarativeforms.com/oauth/airtable` |
| Supported locales | `en`, `es` only |
| Locale resolution order | `?lang=` → browser → `locale` key → `en` |
