<div align="center">

# Declarative Forms

**Forms that live in your Git repo.**

Write a form as a YAML file, commit it to GitHub, and it renders as a live,
hosted form. No visual builder. No vendor lock-in. Your forms are files you own.

[![License: AGPL v3](https://img.shields.io/badge/License-AGPL_v3-542EBC.svg)](https://github.com/declarativeforms/core/blob/main/LICENSE)
[![Self-host with Docker](https://img.shields.io/badge/self--host-Docker%20Compose-0db7ed.svg)](https://github.com/declarativeforms/core#self-hosting)

[Try it on frms.dev](https://frms.dev) · [Source](https://github.com/declarativeforms/core) · [Schema reference](https://github.com/declarativeforms/core/blob/main/SCHEMA.md)

</div>

---

## Forms, the way you already ship software

If you like Tally, Jotform, or Youform, you know the strengths of a good form
builder. Declarative Forms is a different approach, for people who would rather
treat a form like source code.

- **Your forms are files, not rows in someone's database.** Diffable, reviewable, portable.
- **Version control, for real.** Every change is a commit. Review edits in a pull request. Roll back with `git revert`.
- **Preview any branch before it ships.** Add `?branch=my-edit` to a form URL to render that version.
- **Own your responses.** Submissions go to your database. Files go to your storage. Nothing is trapped.
- **Open source and self-hostable.** Run the whole stack with one Docker Compose file. Licensed under AGPL-3.0.

The honest tradeoff: there is no drag-and-drop editor. You write YAML. If your
team lives in Git, that is the point.

## How it works

```yaml
# contact.yaml, committed to your GitHub repo
version: 1
title: "Contact us"
sections:
  - id: contact
    fields:
      - id: email
        type: email
        label: "Email address"
        validators: [required]
      - id: message
        type: long_text
        label: "How can we help?"
        validators: [required]
    next: done
```

Commit that file, then open your form:

```
https://frms.dev/your-org/your-repo/contact
```

A commit is a deploy. That is the whole workflow.

## Explore

| | |
| --- | --- |
| **Try the hosted app** | [frms.dev](https://frms.dev) |
| **Read the source and self-host** | [declarativeforms/core](https://github.com/declarativeforms/core) |
| **Learn the form schema** | [SCHEMA.md](https://github.com/declarativeforms/core/blob/main/SCHEMA.md) |
| **Get started** | [Quick start](https://github.com/declarativeforms/core#quick-start) |

<div align="center">

Built for teams who want their forms under the same review and history as their code.

Licensed under [AGPL-3.0](https://github.com/declarativeforms/core/blob/main/LICENSE).

</div>
