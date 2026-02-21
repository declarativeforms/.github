# Reference Field Authoring Standard

Use this guide when creating or updating any field reference page under `docs/reference/`.

## Goal

Create consistent, neutral, technical reference pages that show field behavior through YAML examples.

## File naming

- Use kebab-case file names.
- Use the pattern: `<field-name>-field.mdx`.
- Example: `short-text-field.mdx`, `long-text-field.mdx`.

Use the field `type` name for file naming:

- `address` -> `address-field.mdx`
- `address_locality` -> `address-locality-field.mdx`
- `address_region` -> `address-region-field.mdx`
- `address_country` -> `address-country-field.mdx`
- `date` -> `date-field.mdx`
- `dropdown` -> `dropdown-field.mdx`
- `email` -> `email-field.mdx`
- `file_upload` -> `file-upload-field.mdx`
- `hidden` -> `hidden-field.mdx`
- `long_text` -> `long-text-field.mdx`
- `mobile_number` -> `mobile-number-field.mdx`
- `multiple_select` -> `multiple-select-field.mdx`
- `number` -> `number-field.mdx`
- `rating` -> `rating-field.mdx`
- `signature` -> `signature-field.mdx`
- `short_text` -> `short-text-field.mdx`
- `single_select` -> `single-select-field.mdx`
- `url` -> `url-field.mdx`

## Required page structure

Every field reference page must follow this exact structure:

1. Frontmatter
2. `## Minimal example`
3. `## Full configuration example`

## Hard rules

- Use YAML examples only.
- Do not use tables.
- Keep language technical and neutral.
- Do not reference the quickstart scenario or any guide scenario.
- The full configuration example must use exactly one section.
- The full configuration example must use multiple field entries to show variants.
- Include only variants supported by the field/type system.
- Field IDs must be sequential (`field_1`, `field_2`, `field_3`, ...).
- Reset ID numbering per code block.

## Variant coverage requirements

For fields that support these options, include variants in this order:

1. Base
2. Placeholder
3. Custom (field-specific properties)
4. Validators
5. Localized
6. `visible_when`

If a field does not support one of these options, omit it and do not invent support.

## Neutral naming convention

- Use neutral labels and values.
- IDs must stay sequential: `field_1`, `field_2`, `field_3`, ...

Avoid domain-specific names tied to examples in other docs pages.

## Copy/paste template

````mdx
---
title: <Field Name>
description: "YAML reference for `type: <field_type>`."
---

## Minimal example

```yaml
version: 1
title: <Field Name> Minimal
sections:
  - id: section_1
    title: Section 1
    fields:
      - id: field_1
        type: <field_type>
        label: Field 1
    next: done
```

## Full configuration example

```yaml
version: 1
title: <Field Name> Full Configuration
sections:
  - id: section_1
    title: Variant Coverage
    fields:
      - id: field_1
        type: <field_type>
        label: Base variant

      - id: field_2
        type: <field_type>
        label: Placeholder variant
        placeholder: Enter value

      - id: field_3
        type: <field_type>
        label: Custom variant
        # Add supported field-specific properties here.

      - id: field_4
        type: <field_type>
        label: Validator variant
        validators:
          - required

      - id: field_5
        type: <field_type>
        label:
          en: Localized variant
          es: Variante localizada

      - id: field_6
        type: <field_type>
        label: Visible when variant
        visible_when: data.field_1 != ""
    next: done
```
````

## Validation checklist (must pass)

- Frontmatter parses successfully.
- Minimal example is neutral and standalone.
- Full example is neutral and one-section only.
- Variant coverage is complete for supported options.
- Variant order is preserved: base -> placeholder -> custom -> validators -> localized -> visible_when.
- IDs are sequential `field_n` and reset per code block.
- No unsupported features are claimed.
- No tables are used.
- All examples are valid YAML syntax.
