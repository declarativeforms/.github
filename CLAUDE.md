# Declarative Forms — Guide Authoring Rules

## Guide Structure

Every guide must follow this exact skeleton:

```
---
title: "Build a [Use Case]" or "Build a [Use Case] with [Capability]"
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
| 1 | Build a Newsletter Signup | Newsletter signup | Form basics | `version`, `title`, `description`, `sections`, `fields`, `validators`, `next` |
| 2 | Build an Event RSVP with Conditional Logic | Event registration | Conditional branching | `next` with `when`/`go`/`else`, multi-section |
| 3 | Build a Feedback Form with Email Notification | Feedback collection | Email connection | `connections`, `type: email`, Handlebars templating |
| 4 | Build a Job Application with File Uploads | Job application | File uploads | `type: file_upload`, `type: mobile_number`, `max` validator |
| 5 | Build a Customer Survey with Ratings | Customer survey | Rating field | `type: rating`, `min_label`, `max_label` |
| 6 | Build a Contact Form with Webhook Integration | Contact form | Webhook connection | `connections`, `type: webhook` |
| 7 | Build a Registration Form with Email Verification | Registration | OTP verification | `otp: true` on email fields |
| 8 | Build a Booking Form in Multiple Languages | Booking | Localization | `locale`, `ILocalizedText`, `?lang=` |
| 9 | Build an Order Form with Conditional Fields | Order form | Conditional field visibility | `visible_when` |
| 10 | Build a Waitlist Signup with a Custom Completion Screen | Waitlist signup | Completion screen | `completion`, `title`, `message`, `button`, `{{data.fieldId}}` |
| 11 | Build a Country Selector with a Searchable Dropdown | Country selector | Searchable dropdown | `type: dropdown`, `searchable: true` |

## Authoring Rules

- **Title pattern**: "Build a [Use Case]" (guide 1) or "Build a [Use Case] with [Capability]" (guides 2+)
- **One capability per guide**: each guide introduces exactly ONE new capability
- **Complete YAML**: the YAML example must be a complete, valid form — never a fragment
- **Semantic IDs**: use `signup`, `name`, `email` — never `section_1` / `question_1`
- **"Deploy it" is identical**: copy-paste the same deploy section across all guides
- **Pure Markdown**: no Mintlify components — use `---` separators between sections
- **Example file**: each guide has a matching `examples/<snake_case>.yaml` file
