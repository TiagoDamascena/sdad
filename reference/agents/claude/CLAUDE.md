# Spec — Claude Code Instructions

## What this repository is

This repository is the single source of truth for the product. It captures what the product does, for whom, and the rules that govern its behavior — independent of how it is implemented.

## Structure

### Root level

- `overview.md` — product vision, business model, target users
- `domain.md` — ubiquitous language and core concepts shared across modules
- `users.md` — user personas and profiles

### modules/{module}/

Everything relevant to a specific domain module:

- `overview.md` — what the module does, its boundaries, and how it relates to other modules
- `domain.md` — concepts specific to this module
- `rules.md` — business rules that apply across multiple use cases within this module
- `use-cases/index.md` — list of all use cases in this module
    - `use-cases/{use-case}.md` — one file per use case: actor, intent, main flow, alternative and exception flows, applicable rules

### templates/

Templates for new files. Always use the appropriate template when creating files.

| Template | Use for |
|----------|---------|
| `templates/use-case.md` | New use case files |
| `templates/module.md` | New module overview files |
| `templates/rules.md` | New rules files |

## Writing conventions

- Filenames in kebab-case: `request-payout.md`, not `Request Payout.md`
- Dates in ISO format: `YYYY-MM-DD`
- Use wikilinks for internal references: `[[note-name]]`
- Use cases must reference applicable rules via wikilinks: `[[rules#rule-name]]`

## Never do

- Do not write or modify anything without explicit user instruction via /consolidate
- Do not delete files without user confirmation
- Do not change the folder structure without updating this file
