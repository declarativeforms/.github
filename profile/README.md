# Declarative Forms

Git-native forms and surveys

Declarative Forms is a developer-first alternative to traditional form platforms. Instead of building forms through visual editors, forms are defined as declarative configuration in a GitHub repository.

This keeps forms in the same workflow as the rest of your system: explicit source, version history, diffs, and review.

## Quick Start

Transform a GitHub repository into a form engine in under 60 seconds.

### 1. Add a config file

Create a file named `feedback.yaml` in the root of your repository:

```yaml
version: 1
title: "Quick Feedback"
description: ""
sections:
  - id: main
    fields:
      - id: feedback
        type: long_text
        label: "What can we improve?"
    next: done

connections:
  - type: webhook
    url: https://your-api.com/hooks/form
```

### 2. Push to GitHub

Commit and push the file to your repository.

### 3. Open your form

Your form is live immediately at:

`https://app.declarativeforms.com/<owner>/<repository>/feedback`

## Why Declarative Forms

Form builders work well when forms are simple. As soon as forms become part of real workflows and need to change over time, UI-first tools start to hide the structure and make change tracking harder.

Declarative Forms makes the form definition explicit and versioned, so forms can be maintained with the same discipline as the rest of a codebase.

## The 48-Hour Promise

Most form platforms have feature request boards where ideas go to die. Hundreds of requests, some over 18 months old, sitting in a backlog that never moves.

We do things differently. Open a [GitHub Issue](https://github.com/declarativeforms/.github/issues) with your feature request — if it genuinely improves the product, we'll ship it within 48 hours.

No waitlists. No roadmap purgatory. No "we'll consider it." Just open an issue and watch it get built.
