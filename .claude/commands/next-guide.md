# /next-guide — Automated Guide Authoring

You are writing the next guide for the Declarative Forms docs site. Follow these five phases exactly. Do NOT skip phases or combine them. Show your reasoning at each step.

---

## Phase 1 — Discover All Capabilities from Source Code

Explore the source code to build a complete inventory of every documentable capability. Start from these three entry points and follow references deeper as needed:

- **`core/src/components/declarative-form/`** — types, field components, validation logic
- **`api/src/core/`** — connection types, services (email, OTP, webhooks)
- **`examples/*.yaml`** — real-world usage of every capability

### How to explore

1. **Glob for type definitions** in the entry-point directories, read them, and extract every field type, validator, modifier, connection type, and form-level property
2. **Follow references into implementation files** — field components, validation functions, services — to understand *runtime behavior*, not just type signatures
3. **Read the example YAML files** to see how capabilities are actually used in practice

### What to look for

Build your own inventory organized by these categories:

- **Field types** — every distinct `type` value a field can have
- **Field modifiers** — per-field properties that alter behavior (e.g., `otp`, `visible_when`, `searchable`)
- **Validators** — validation rules and how their behavior varies by field type (e.g., `max` may mean different things on `file_upload` vs `short_text` vs `rating`) — read the validation implementation, not just the type
- **Connections** — integration types and their configuration
- **Form-level features** — properties on the form itself (completion, scheduling, locale, analytics)
- **URL features** — query-parameter-driven behavior (prefill, language, reserved params)

Output a full inventory table before moving on.

---

## Phase 2 — Audit Existing Guides

Read every file in `docs/guides/*.mdx`.

For each guide, extract:
1. The title and the **primary capability** it teaches
2. Every YAML property and concept used in its example code block

Output a "covered capabilities" set — everything already taught across all existing guides.

---

## Phase 3 — User-Value Analysis & Capability Selection

Compute: **uncovered** = (Phase 1 inventory) minus (Phase 2 covered set).

### Step 3a — Score each uncovered capability

For every uncovered capability, evaluate and score 1–5:

| Criteria | Question |
|----------|----------|
| **Reach** | What percentage of form builders would need this? |
| **Pain without it** | How much does a builder struggle without documentation for this? |
| **Real-world use cases** | How many distinct, practical form types does this enable? |
| **Coverage gap** | Is this completely undocumented, or partially covered elsewhere? |

Output a ranked table with scores and totals.

### Step 3b — Select the winner

From the ranked table, pick the highest-scoring capability. Apply these tiebreakers:

1. **Builds on prior knowledge** — reuses concepts from earlier guides, introduces exactly ONE new thing
2. **Unlocks future guides** — opens the door to related features
3. **Has a reference example** — prefer capabilities with a matching `../examples/*.yaml` file

Output: the winning capability, the use case, the proposed title (following the pattern "Build a [Use Case] with [Capability]"), and a one-sentence justification.

---

## Phase 4 — Write the Guide

Create three outputs. Follow the authoring rules in CLAUDE.md exactly.

### 4a. Guide file: `docs/guides/<kebab-case>.mdx`

Use this exact skeleton:

```
---
title: "<your title>"
description: <one sentence — what the reader will build>
---

<Outcome statement: 1-2 sentences saying what you'll build + what capability you'll learn>

---

## Define the form

Create a file called `<snake_case>.yaml` in your repository:

\`\`\`yaml
<complete, valid YAML — version: 1, semantic IDs, proper next>
\`\`\`

---

## Deploy it

Commit and push the file to your repository:

\`\`\`bash
git add <snake_case>.yaml
git commit -m "add <description> form"
git push
\`\`\`

Then open your form at:

\`\`\`
https://app.declarativeforms.com/<organization>/<repository>/<snake_case>
\`\`\`

(The `.yaml` extension is not included in the URL.)
```

Rules:
- **One capability per guide**: introduce exactly ONE new concept
- **Complete YAML**: must be a full, valid form — never a fragment
- **Semantic IDs**: use meaningful IDs like `signup`, `name`, `email` — never `section_1` / `question_1`
- **Pure Markdown**: no Mintlify components (`<Card>`, `<Tabs>`, etc.) — use `---` separators
- **Deploy section is identical** across all guides (only the filename changes)

### 4b. Example file: `examples/<snake_case>.yaml`

Write the exact same YAML from the guide as a standalone file.

### 4c. Update `docs/docs.json`

Add the new guide slug (`"guides/<kebab-case>"`) to the end of the Guides `pages` array.

---

## Phase 5 — Validate & Update CLAUDE.md

### Factual review of guide prose

Before checking YAML properties and validators, verify every prose claim in the guide:

1. **Re-read the generated guide file** end-to-end — the outcome statement, description, and every sentence that describes what the platform does or what the reader will achieve
2. **Extract every factual claim** — list each statement that asserts a platform capability, behavior, or integration
3. **Verify each claim against source code** — grep and read the implementing code to confirm the claim is accurate and supported
4. **Check scope** — ensure the guide doesn't imply the platform can do things it can't (e.g., direct third-party integrations when it only provides generic webhooks, or features that require external tools without saying so)
5. **Fix inaccuracies** — rewrite any claim that is misleading, overstated, or unsupported by source code

Only proceed to source-code verification once every prose claim is confirmed accurate.

### Source-code verification

Before running structural checks, grep and read the source code to verify every claim the guide makes:

- [ ] **Validators match field type** — grep for each validator used in the guide, read the validation implementation, and confirm prose matches what the validator actually does for that specific field type
- [ ] **Field modifiers match components** — grep for each field modifier, read the implementing component, and confirm behavior description is accurate
- [ ] **Prose claims match code** — for every sentence describing what a YAML property does, find and read the implementing source code to verify accuracy
- [ ] **No invented behavior** — confirm the guide doesn't describe behavior that doesn't exist in source code

### Structural validation checklist

Run through every item. If any check fails, fix it before proceeding.

- [ ] Frontmatter has `title` + `description`
- [ ] Title matches "Build a [Use Case]" or "Build a [Use Case] with [Capability]"
- [ ] Exactly two `##` headings: `## Define the form` and `## Deploy it`
- [ ] One complete YAML block with `version: 1`, semantic IDs, proper `next`
- [ ] Deploy section matches the standard template (only filename differs)
- [ ] No Mintlify components (no `<Card>`, `<Tabs>`, etc.)
- [ ] `examples/<snake_case>.yaml` matches guide YAML exactly
- [ ] `docs/docs.json` is valid JSON with the new slug present in the Guides pages array

### Update CLAUDE.md

Open `/Users/barenderasmus/development/examples/.github/CLAUDE.md` and add or update a row in the **Guide Roster** table for the new guide. Include: number, title, use case, capability introduced, and key concepts.

---

## Final Output

After all five phases, summarize:
1. What capability was selected and why
2. The files created/modified
3. The validation checklist results (all must pass)
