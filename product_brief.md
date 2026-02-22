# Declarative Forms Documentation Product Brief and Prompting Ruleset

## 1. Purpose of This Document

This file is the canonical internal brief for creating and maintaining Declarative Forms documentation.

It combines:

- product context and positioning
- repo-grounded feature constraints
- documentation information architecture guidance
- writing standards by page type
- prompting rules and execution workflow for future documentation tasks

Use this file as the default source when prompting an agent or collaborator to create, revise, or review docs for this project.

## 2. Source-of-Truth Policy (Strict)

Documentation content must be grounded in verifiable sources.

### Primary repositories (must analyze before substantial doc work)

- `/Users/barenderasmus/development/examples/api`
- `/Users/barenderasmus/development/examples/core`
- `/Users/barenderasmus/development/examples/examples`

### Source precedence

1. `core` (primary for user-facing schema/capabilities)
2. `api` (cross-check overlapping types and payload shapes)
3. `examples` (syntax patterns and practical YAML examples)

### Non-negotiable rules

- Do not invent features.
- Do not claim behavior that is not explicit in code/examples.
- When uncertain, inspect the repos before writing.
- Prefer examples and references grounded in supported schema and runtime behavior.

## 3. Product Overview (Approved Positioning)

Declarative Forms is a developer-first form system where forms are defined in YAML and rendered as hosted forms.

Core workflow:

1. Write a YAML form file
2. Push it to a public GitHub repository
3. Open the hosted form URL
4. The app reads the YAML and renders the form

Hosted URL pattern used in docs:

`https://app.declarativeforms.com/{owner}/{repository}/{file}`

The filename becomes the form path segment without the `.yaml` extension.

## 4. Problem Framing (Docs-Safe Messaging)

### What problem the product solves

Traditional form tools typically depend on UI builder workflows. This creates friction for developers and Git-first teams who prefer explicit, versioned definitions and text-based workflows.

Declarative Forms lets teams define forms in source files and manage changes with standard engineering practices (commits, diffs, review).

### Messaging themes that are acceptable

- declarative / code-first form authoring
- Git-native workflow alignment
- clear source definitions instead of builder state
- developer workflow compatibility
- LLM-assisted generation compatibility (when phrased as workflow fit, not guaranteed automation outcomes)

### Messaging themes to avoid

- unsupported claims about platform internals
- claims about behavior not verified in code/examples
- implementation details not relevant to users (unless writing internal docs)

## 5. Verified Capability Summary (Repo-Grounded)

### 5.1 Form model

Top-level form supports (as seen in `core` and cross-checked in `api`):

- `id` (optional)
- `version`
- `title`
- `description` (optional)
- `sections`
- `completion` (optional)
- `connections` (supported connection variants are defined)
- `start_date` (optional)
- `end_date` (optional)
- `locale` (supported in `core`)
- `mixpanel` (optional)

### 5.2 Section model

Each section includes:

- `id`
- `title`
- `fields`
- `next`

Supported `next` shapes:

- `done`
- a section ID string
- an HTTPS URL string
- a rule list containing ordered `when`/`go` entries and optional `else`

Behavior used in docs:

- rules are evaluated in order
- first matching `when` wins
- `else` returns when reached
- fallback is `done` if no rule matches and no `else` exists
- external redirect behavior is recognized for `https://` values

### 5.3 Field model (common properties)

Common field-level properties include:

- `id`
- `type`
- `label`
- `placeholder` (where supported)
- `validators`
- `options` (selection types)
- `visible_when`

Field-specific capabilities supported in schema include examples such as:

- `otp` on email
- `searchable` on dropdown
- `outputFormat` on address
- `min_label` / `max_label` on rating

### 5.4 Supported field types (current reference set)

- `address`
- `address_locality`
- `address_region`
- `address_country`
- `date`
- `dropdown`
- `email`
- `file_upload`
- `hidden`
- `long_text`
- `mobile_number`
- `multiple_select`
- `number`
- `rating`
- `signature`
- `short_text`
- `single_select`
- `url`

### 5.5 Connections (supported variants)

Supported connection types in schema:

- `webhook`
- `email`
- `airtable`

## 6. Current Documentation IA (Target State)

### 6.1 Getting Started

- `Introduction`
- `Quickstart`

### 6.2 Templates

Templates are copy-ready YAML examples intended for practical reuse.

Current Templates section contains 3 pages:

- Client Intake Form Template
- Event Registration and RSVP Form Template
- Feedback and Feature Request Form Template

### 6.3 Reference

Reference pages are technical and example-driven.

They include:

- top-level object references (`Form Reference`, `Section Reference`)
- field references for all supported field types

### 6.4 Help

Support and project assistance links/pages.

## 7. Documentation Writing Principles

### 7.1 Universal standards

- Be clear, concise, and easy to scan.
- Prefer concrete examples over abstract descriptions.
- Keep claims factual and repo-verifiable.
- Keep page scope narrow and intentional.
- Maintain structural consistency across similar page types.

### 7.2 Developer-first tone

Use a direct, developer-friendly voice.

Preferred tone traits:

- explicit
- practical
- concise
- technical without unnecessary jargon

Avoid:

- vague marketing copy
- over-explaining obvious YAML mechanics
- unsupported comparisons or claims

## 8. Page-Type Standards

## 8.1 `Introduction` page (`docs/getting-started/introduction.mdx`)

Purpose:

- First-touch explanation of the product
- Problem framing + product value
- High-level how-it-works summary

Required content:

- what the product is
- what problem it solves
- why it differs from UI-first form builders
- core value proposition
- high-level workflow

Constraints:

- keep examples minimal
- focus on framing and onboarding, not exhaustive feature coverage
- preserve a clear link to Quickstart

## 8.2 `Quickstart` page (`docs/getting-started/quickstart.mdx`)

Purpose:

- fastest path to understanding and using the product

Default structure:

1. Create a YAML file
2. Push to GitHub
3. Open the hosted form URL

Constraints:

- one simple working example
- minimal explanation
- no feature overload
- explain the core file-to-hosted-form relationship clearly

## 8.3 Template pages (`docs/templates/*.mdx`)

Purpose:

- copy-ready starting points users can adapt

Current standard (strict):

- frontmatter only (`title`, `description`)
- one YAML code block
- no prose sections

### Template naming rules (strict)

- Title pattern: `<Use Case> Template` or `<Use Case> Form Template` (use one consistent pattern across the set)
- Description pattern: `YAML template for <outcome>.`
- Keep titles and descriptions structurally consistent across all template pages

### Template content rules

- Full YAML templates are allowed and encouraged
- Optional advanced capabilities may be shown as commented YAML blocks
- Use only supported features
- Prefer reusable templates over overly domain-specific branding/copy

## 8.4 Reference pages (`docs/reference/*.mdx`)

Purpose:

- technical reference documentation
- example-driven schema coverage

Reference constraints:

- YAML examples only
- no tables (for field and object reference pages in the docs set)
- minimal prose
- consistency in headings and frontmatter

Field reference pattern (strict):

- `## Minimal example`
- `## Full configuration example`

Object references (`Form Reference`, `Section Reference`) should match the same heading pattern.

## 8.5 Public GitHub profile README (`profile/README.md`)

Purpose:

- explain the product on the public GitHub profile page
- activate visitors quickly

Recommended structure:

1. title + short tagline
2. product overview
3. quick start
4. why / problem framing
5. links (docs/app/examples)
6. 48-hour promise (if retained)

Avoid turning the profile README into a full docs index.

## 9. Prompting Ruleset for Future Documentation Tasks

This section defines the default behavior for future prompts that ask an agent to create or revise docs.

### 9.1 Default process (strict by default, overridable)

Unless the user explicitly requests a smaller process, use this workflow:

1. Analyze the task and break it into workstreams.
2. Inspect the source repos and current docs before writing.
3. Ask clarifying questions for high-impact ambiguities.
4. Define writing style/tone when requested or when scope is broad.
5. Produce draft(s) when the task is strategic or content-heavy.
6. Review for factual accuracy, scope control, and consistency.
7. Validate navigation paths, frontmatter, and syntax.

The user may explicitly ask to skip or compress parts of this workflow.

### 9.2 Clarifying question standards

Ask clarifying questions when answers materially affect:

- page structure
- audience targeting
- examples and use-case selection
- scope boundaries
- naming or information architecture
- strictness of style/format constraints

Do not ask questions that can be answered by inspecting:

- repo code
- examples
- current docs files
- navigation config

When the user requests a highly planned, multi-step change, ask multiple focused questions per step/workstream.

### 9.3 Drafting and review standards

For complex docs tasks:

- prefer draft-first, then refine
- compare alternatives when positioning or IA is uncertain
- perform a final consistency pass across related pages

For narrow docs tasks:

- make the change directly
- still validate syntax, nav paths, and schema accuracy

### 9.4 Anti-hallucination rules

- Every feature claim must map to code or examples.
- Do not infer product behavior from competitor expectations.
- If a behavior is implementation detail and not user-relevant, omit it from user docs unless explicitly requested.
- If schema support differs between `core` and `api`, treat `core` as primary for docs and note uncertainty internally if needed.

## 10. Documentation Task Checklists

### 10.1 New page checklist

- Frontmatter is valid
- Title/description follow local page-type pattern
- Page scope is clear and narrow
- Examples are repo-grounded
- Links/paths resolve
- Copy is consistent with adjacent pages

### 10.2 Reference page checklist

- `Minimal example` and `Full configuration example` headings are present
- YAML syntax is valid
- No unsupported properties appear
- Naming/variant ordering is consistent with the reference set
- Page remains technical and concise

### 10.3 Template page checklist

- Frontmatter only + one YAML block (current standard)
- Title/description match the strict template pattern
- YAML is copyable and coherent
- Optional features are clearly commented
- No unsupported schema features are shown

### 10.4 Quickstart checklist

- One working example only
- 3-step publish flow is clear
- URL mapping from filename is clear
- No unnecessary feature overlap

## 11. Review and Consistency Expectations

When modifying multiple pages in one task:

- review pages together, not in isolation
- align title/description patterns across siblings
- keep example naming conventions consistent where useful
- avoid introducing multiple styles for the same page type

When asked to "only change what is needed":

- prioritize factual errors, syntax issues, and structural mismatches
- avoid broad rewrites unless inconsistency materially harms usability

## 12. Maintenance Notes

- Update this document when the docs IA changes (for example, Guides -> Templates).
- Update the field type list if schema support changes.
- Keep page-type standards aligned with the actual docs files.
- Keep this file practical for prompting, not just descriptive.
