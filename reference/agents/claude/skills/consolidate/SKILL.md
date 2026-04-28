---
name: consolidate
description: "Persist knowledge from the current session into the spec repository"
trigger: /consolidate
disable-model-invocation: true
---

# /consolidate

Persist knowledge from the current session into the spec repository.

## Step 1 — Identify what to consolidate

Review the entire session and identify everything worth persisting.

Use the classification guide in Step 2 to evaluate each candidate. Apply these filters before adding anything to the list:

**Include:**
- Business rules and domain constraints that govern product behavior
- Use cases that describe actors, flows, and scenarios
- Cross-cutting rules that apply to multiple use cases or modules
- Non-obvious context about a module: its purpose, how it relates to other modules, relevant external integrations and what the product does with them
- Domain concepts and vocabulary specific to the product or a module

**Exclude:**
- Technical details of external services that belong to that service's own documentation
- Anything discoverable by reading the code (model fields, controller structure, route definitions)
- Implementation details with no reuse value outside this specific feature
- Repo-specific context (setup, conventions, tech debt) — that belongs in the repository's own documentation

Present the filtered list to the user:

> "I found the following items to consolidate from this session. Let me know if anything should be removed or added before I proceed."

Wait for the user's confirmation before proceeding.

## Step 2 — Determine the target location

For each item, use the following classification guide:

### modules/{module}/use-cases/{use-case}.md
A specific user-facing flow within a module. The test: does it describe an actor, an intent, a sequence of steps, and what can go wrong? Use one file per use case.
Use template: `templates/use-case.md`

When adding a new use case, always update modules/{module}/use-cases/index.md with a link and brief description.

### modules/{module}/rules.md
Business rules that apply across multiple use cases within the module. The test: is this rule referenced in more than one use case? If a rule only applies to a single use case, it belongs in that use case's pre-conditions — not here.

### modules/{module}/overview.md
Non-obvious context about the module: what it does, its boundaries, how it relates to other modules, relevant external integrations and what the product does with them.

### modules/{module}/domain.md
Concepts and vocabulary specific to this module. Terms that have a precise meaning within this module's context.

### domain.md
Core domain concepts and ubiquitous language that appear across multiple modules. Terms that have a specific meaning in this product that differs from common usage.

### users.md
User personas and profiles. The test: does this describe who uses the product, their goals, and their context in a way that is not specific to any single module?

## Step 3 — Draft all content

Draft all notes at once using the appropriate template from the `templates/` folder where available. For rules, module overviews, and domain files, let the content dictate the structure.

For all notes:
- Write concise, self-contained content
- Avoid referencing the conversation — every note must make sense on its own
- Cross-reference applicable rules in use cases using wikilinks: `[[rules#rule-name]]`

## Step 4 — Confirm before writing

Show all drafted notes with their target file paths in a single review.
The user may approve all, remove specific items, or request changes to any note.

Only write to the spec after explicit user approval.

## Step 5 — Write to the spec

Write all confirmed files in one pass.

Use kebab-case filenames for all files.

If any target file already exists, update the relevant sections rather than replacing the entire file. Show the diff to the user before applying.

## Rules

- Never write to the spec without explicit user confirmation in Step 4
- Never invent information not present in the session
- If the session does not contain enough context to write a good note, say so and ask the user to provide more detail
