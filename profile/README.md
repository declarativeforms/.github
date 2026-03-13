# Declarative Forms

**Define forms in YAML. The platform renders the experience.**

## What is Declarative Forms?

Declarative Forms is a developer-first alternative to visual form builders like Typeform, Google Forms, and JotForm. Instead of dragging and dropping in a visual editor, you define your form in a YAML file and the platform handles rendering, validation, submissions, and post-submit actions. Your form definitions live in GitHub, giving you version history, collaboration, and a repeatable workflow.

## Key Features

- **18 field types** — text, email (with OTP verification), rating, file upload, address, geolocation, signature, hidden, and more
- **Multi-step forms** — split forms into sections with controlled navigation and branching
- **Conditional visibility** — show or hide fields based on previous answers
- **Completion screens** — customize what users see after submitting, with data interpolation
- **Post-submit actions** — send confirmation emails, trigger webhooks, and connect to external services
- **Analytics** — built-in Mixpanel integration for tracking form interactions
- **GitHub workflow** — forms are YAML files in your repo — edit, review, and deploy with your existing tools

## Quick Example

```yaml
version: 1
title: "Feedback"
description: "Help us improve our product!"

sections:
  - id: section_1
    title: "Section 1"
    fields:
      - id: question_1
        type: email
        label: What's your email?
        placeholder: hello@declarativeforms.com
        validators:
          - required
    next: done

connections:
  - type: email
    to: "{{data.question_1}}"
    subject: Thanks for your submission
    body: |
      Hi {{data.question_1}}, we received your response.
```

Save this as `feedback.yaml` in your repo, then open it at:

```
https://frms.dev/<org>/<repo>/feedback
```

## Who is it for?

Declarative Forms is built for teams that manage multiple forms as part of an operational workflow or product experience. It is a strong fit when you need consistency across forms, want a structured and repeatable process for defining them, and prefer working in code over visual editors.

## Links

- [Documentation](https://docs.declarativeforms.com)
- [Open the App](https://frms.dev)
- [GitHub](https://github.com/declarativeforms)
- [Support & Issues](https://github.com/declarativeforms/.github/issues)
