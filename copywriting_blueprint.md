# Copywriting Blueprint — Declarative Forms

This blueprint is the single source of truth for writing all product copy. It covers both marketing-style content (Getting Started pages, README, landing pages) and technical documentation (Concept pages, reference material). Any writer should be able to produce on-brand, consistent content using only this document.

---

## 1. Purpose

This blueprint ensures that every piece of written content for the product is:

- **Consistent** — same voice, structure, and terminology across all pages
- **Audience-appropriate** — marketing content inspires action, technical content builds competence
- **Accurate** — every claim and example reflects the actual product behavior
- **Scannable** — readers find what they need in seconds, not minutes

---

## 2. Audience

### Primary audience

Developers and technical team leads who currently build or maintain forms as part of their products or workflows. They are comfortable with Git, YAML, and code editors. They may be evaluating alternatives to visual form builders or looking for a way to bring forms into their existing development workflow.

### Audience states

Copy should account for where the reader is in their journey:

| State | Description | Content goal |
|---|---|---|
| **Unaware** | Has not heard of the product | Create curiosity, establish relevance |
| **Aware** | Knows the product exists, exploring | Communicate the value proposition clearly |
| **Evaluating** | Comparing options, reading docs | Build confidence through clarity and completeness |
| **Onboarding** | Setting up their first form | Remove friction, deliver a quick win |
| **Building** | Creating real forms for production | Provide precise, reliable reference material |

---

## 3. Voice and Tone

### Voice (constant across all content)

The product voice is **clear, confident, and direct**. It speaks as a knowledgeable peer, not a teacher or a salesperson. It respects the reader's intelligence and time.

Principles:

- **Say it once, say it well.** No filler sentences. No restating the same idea in different words.
- **Lead with what matters.** The first sentence of every paragraph should carry meaning.
- **Be concrete.** Prefer "a YAML file in your repository" over "a configuration-driven approach."
- **Assume competence.** The audience knows Git, knows YAML, and has built software before. Do not explain these prerequisites.

### Tone (varies by content track)

| Track | Tone | Characteristics |
|---|---|---|
| **Marketing** (Getting Started, README) | Confident and inviting | Benefit-led, forward-looking, creates momentum. Uses "you" frequently. Short paragraphs. Emphasizes simplicity and speed. |
| **Technical** (Concepts, reference) | Precise and supportive | Structure-led, factual, builds understanding layer by layer. Uses second person sparingly. Longer paragraphs when needed for completeness. Emphasizes correctness and clarity. |

### What to avoid

- **Hype and superlatives.** Not "revolutionary," "game-changing," or "blazing fast."
- **Hedging.** Not "you might want to consider," "it's possible that." Be direct.
- **Jargon without context.** If a term is specific to the product, define it on first use. If it is general knowledge for the audience (e.g., YAML, Git, webhook), do not define it.
- **Excessive bullet points.** Bullets are for lists of parallel items. Explanations belong in prose.
- **Cross-references as crutches.** Each page should make sense on its own. Do not lean on "as described in [other page]" to complete an explanation.

---

## 4. Messaging Hierarchy

These messages cascade from general to specific. Higher-level messages inform lower-level ones.

### Level 1 — Positioning statement

Forms defined as configuration in a Git repository. Versioned, reviewable, and deployable like the rest of your codebase.

### Level 2 — Core value pillars

1. **Declarative** — Define what the form should be, not how to build it. The schema is the form.
2. **Git-native** — Forms live in your repository. Changes are commits. Reviews are pull requests.
3. **Developer-first** — Built for people who work in code editors, not drag-and-drop builders.

### Level 3 — Capability themes

These are the areas that copy can draw from when explaining what the product offers:

- Multi-section forms with configurable flow
- Rich field types that cover real-world data collection
- Validation rules that are declared, not coded
- Conditional logic for dynamic form behavior
- Multiple data destinations (connections)
- Localization built into every text property
- Dynamic text through templating
- Analytics integration
- Time-bounded form availability

---

## 5. Content Tracks

### Marketing Track

**Used for:** Getting Started pages, README, landing pages, feature highlights, onboarding emails

**Primary goal:** Move the reader from their current state (unaware/aware/evaluating) toward onboarding. Create the "AHA moment" — the point where they understand the value and want to try it.

**Structure pattern for Getting Started pages:**

```
---
title: [Short, noun-based title]
description: [One sentence. Understandable without context. No jargon.]
---

[Opening paragraph — what this is and why it matters. 2-3 sentences max.]

---

## [First concept or step]

[Explanation that builds understanding. Lead with the benefit or outcome, then show how.]

[YAML example if relevant — keep it minimal, show only what this section covers.]

---

## [Next concept or step]

[Continue building. Each section should feel like a natural next step.]

---
```

**Writing rules for Marketing Track:**

1. Open with the outcome, not the mechanism. "Your form is live at a URL" before "here's how the routing works."
2. Use one YAML example to demonstrate, not to exhaustively document.
3. Every section should earn the reader's continued attention. If a section does not make them more excited or more confident, cut it.
4. Paragraphs should be 1-3 sentences. White space is a feature.
5. End with momentum — the reader should know exactly what to do next.

### Technical Track

**Used for:** Concept pages, reference documentation, how-to guides

**Primary goal:** Build the reader's understanding and competence. Each concept page should leave the reader confident they can use that concept correctly in their own forms.

**Structure pattern for Concept pages:**

```
---
title: [Concept name — singular noun or noun phrase]
description: [One sentence. Explains what it is without assuming prior reading.]
---

[Introduction — 2-3 paragraphs explaining the concept in plain language. What is it, what role does it play, and why does it exist. This is where the reader builds their mental model. No YAML here.]

---

## Structure

[A focused YAML block showing only the properties relevant to this concept. Omit properties that belong to other concept pages. Use comments sparingly — only where the YAML itself is not self-explanatory.]

```yaml
[focused YAML example]
```

---

## [Property name]

[1-2 paragraphs explaining this property: what it does, what values it accepts, and how it affects the form. Use a short inline YAML snippet if it clarifies the explanation.]

## [Next property name]

[Same pattern. One section per property shown in the Structure block.]

---
```

**Writing rules for Technical Track:**

1. The introduction creates understanding. The Structure section shows the shape. The property sections build competence. Maintain this progression.
2. The Structure YAML block is a **focused view** — it includes only the properties explained on this page. Properties that belong to other concepts (e.g., field-level details on a sections page) should be omitted or shown as `# ...` placeholders.
3. Explain properties in the order they appear in the Structure YAML.
4. Each property explanation should answer: What is it? What values can it have? What does it affect?
5. Use inline YAML snippets within property explanations to show specific values or variations.
6. Do not reference other concept pages. Each page is self-contained.

---

## 6. YAML Conventions

YAML is the product's primary interface. How code blocks appear in documentation directly affects comprehension.

### When to show YAML

- **Concept pages:** One Structure block per page, plus inline snippets within property explanations.
- **Getting Started pages:** One or two examples maximum. Show complete, runnable forms — the reader should be able to copy-paste and see results.
- **Reference pages:** Complete schema examples with all properties shown.

### How to format YAML blocks

- Use `yaml` language tag for syntax highlighting.
- Indent with 2 spaces (matches the product's convention).
- Omit properties that are not relevant to the current explanation.
- Use `# ...` to indicate omitted sections only when the reader needs to understand that more exists.
- Use realistic but simple values. "Feedback Survey" not "Test Form 1."
- Keep examples to 15-25 lines where possible. Longer examples should be broken into annotated sections.

### Inline snippets

For explaining a single property or a small variation, use inline YAML within the prose:

```yaml
next: done
```

This is preferable to describing the syntax in words ("set the next property to the string done").

---

## 7. Terminology

Consistent terminology prevents confusion and builds recognition. Use these terms exactly as written.

| Term | Usage | Do not use |
|---|---|---|
| form | The top-level entity. A complete form definition. | survey, questionnaire (unless quoting a user) |
| section | A step or page within a form. Contains fields and defines navigation. | step, page, screen (except "completion screen") |
| field | A single input element within a section. | input, control, element, widget |
| field type | The kind of field (e.g., short_text, email). Always use the exact type name in backticks when referencing a specific type. | field kind, input type |
| schema | The YAML definition of a form. | config, spec, manifest (these carry Kubernetes connotations) |
| connection | A data destination configured in the form schema. | integration, sink, output |
| completion screen | The screen shown after form submission. | thank-you page, success page, done screen |
| validator | A validation rule declared on a field. | validation, constraint |
| `when`/`go`/`else` | Conditional navigation keywords used in the array form of `next`. Always in backticks. | branching rules, routing conditions |
| visible_when | The conditional visibility expression. Always in backticks. | visibility rule, show condition |
| next | The navigation property on a section. Always in backticks. | routing, flow, navigation (except in general explanations) |
| compilation | The process of resolving a schema into a renderable form. | rendering, processing, building |

### Casing rules

- Product name: **Declarative Forms** (title case, two words)
- Feature names: lowercase unless starting a sentence. "conditional logic," not "Conditional Logic."
- YAML property names: always in backticks, always lowercase with underscores. `start_date`, `visible_when`, `next`.
- Field type names: always in backticks. `short_text`, `email`, `file_upload`.

---

## 8. Page Metadata

Every Mintlify page starts with frontmatter. Follow these rules:

### Title

- Concept pages: The concept name as a noun or noun phrase. "Sections" not "Working with Sections" or "How Sections Work."
- Getting Started pages: Action-oriented or noun-based. "Introduction" or "Quickstart."
- Maximum 3 words.

### Description

- One sentence, maximum 15 words.
- Must make sense without having read any other page.
- No jargon. No product-specific terms that are not self-explanatory.
- Ends with a period.

---

## 9. Quality Checklist

Before publishing any page, verify:

**Content:**
- [ ] Every claim is accurate against the current codebase
- [ ] YAML examples are valid and would produce working forms
- [ ] No properties are shown that do not exist in the schema
- [ ] No features are described that do not exist in the product

**Structure:**
- [ ] Page follows the correct track template (Marketing or Technical)
- [ ] Frontmatter title and description follow the metadata rules
- [ ] YAML blocks follow the formatting conventions
- [ ] Properties are explained in the order they appear in the Structure block

**Voice and Tone:**
- [ ] Matches the track tone (confident/inviting for marketing, precise/supportive for technical)
- [ ] No hype, hedging, or unnecessary jargon
- [ ] First sentence of each paragraph carries meaning
- [ ] No unexplained product-specific terms

**Self-containment:**
- [ ] Page makes sense without having read any other page
- [ ] No "as described in [other page]" references
- [ ] Introduction creates sufficient context for everything that follows

**Conciseness:**
- [ ] No filler sentences
- [ ] No repeated ideas in different words
- [ ] Paragraphs are appropriately sized (1-3 sentences for marketing, 1-5 for technical)
- [ ] YAML examples show only what is relevant

---

## 10. Progressive Disclosure Model

The documentation follows a deliberate progression that mirrors the reader's journey from curiosity to competence.

### Getting Started (Marketing Track)

These pages answer: **"What is this and should I care?"**

The reader arrives with curiosity or a problem to solve. They leave with understanding of the value proposition and a working first form. The tone is inviting, the examples are complete but minimal, and the focus is on outcomes.

**Introduction** → Establishes what the product is, why it exists, and what makes it different. Creates the first "AHA moment": the realization that forms can be defined as versionable configuration.

**Quickstart** → Delivers the second "AHA moment": a working form in under 60 seconds. The reader experiences the product's core promise firsthand.

### Concepts (Technical Track)

These pages answer: **"How does this actually work?"**

The reader has decided to invest time learning. They need to build a mental model of the product's structure and capabilities. Each page covers one concept completely, with focused YAML examples and property-level explanations.

The concept pages are ordered to build understanding progressively:

1. **Forms** → The container. Everything starts here.
2. **Sections** → The building blocks inside a form. Single and multi-section patterns.
3. **Fields** → The inputs inside sections. Core field structure without exhaustive type coverage.
4. **Validation** → Rules that fields can declare. Follows naturally from fields.
5. **Completion** → What happens after submission. Closes the basic form lifecycle.
6. **Connections** → Where data goes. Extends the form beyond display.
7. **Conditional Logic** → Dynamic behavior: section branching and field visibility.
8. **Templating** → Dynamic text using form data.
9. **Localization** → Multi-language support for every text property.
10. **Analytics** → Tracking form usage.

This order moves from structural concepts (what is a form made of?) to behavioral concepts (what can a form do?) to operational concepts (how do I manage a form in production?).
