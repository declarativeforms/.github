# Docs CLAUDE.md

This docs site is built with [Mintlify](https://mintlify.com).

## Structure

- `getting-started/` — Introduction, Quickstart, How It Works
- `guides/` — 30 step-by-step guides organized in 4 groups:
  - Building the Form (17 guides, one per field type or form feature)
  - Form Behavior (6 guides)
  - Connections (5 guides)
  - Localization and Analytics (2 guides)
- `reference/` — YAML schema reference + 16 field type reference pages
- `help/` — Support page

## The canonical example form

All guides build on `rental.yaml` — a rental application form. Each guide adds exactly one feature. The quickstart shows the minimal 3-field version; the final guide completes the form with all features.

## Guide format rules

Every guide follows this exact structure:

1. Frontmatter (`title`, `description`)
2. One-sentence intro
3. `## What to add` — minimal YAML delta only (never the full form)
4. `## How it works` — explanation of the new feature
5. `Next:` link to the following guide (except the last guide)

No guide may contain a "Complete rental.yaml" block.

## Running locally

```bash
cd docs
mintlify dev
```

## Navigation

Navigation is defined in `mint.json`. All 30 guide slugs and 17 reference slugs must be registered there.
