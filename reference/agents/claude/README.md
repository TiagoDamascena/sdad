# Claude Code

This folder contains the configuration files needed to connect Claude Code to your spec repository.


## How it works

Claude Code reads the spec before acting. This is achieved through two mechanisms:

- **A section in the `CLAUDE.md` of each code repository:** points Claude to the spec and instructs it to read the relevant sections before starting any task or making any decision.
- **`additionalDirectories` in `settings.json`:** makes the spec repository available to Claude Code sessions running in each code repository, enabling Claude to read the spec.

Together, these ensure that Claude always has the necessary product context before writing or modifying any code.


## Bidirectional sync

Keeping the spec and implementation in sync is the engineer's responsibility. Claude Code assists with the spec side through the `/consolidate` skill:

- At the end of a working session, the engineer runs `/consolidate`
- Claude reviews the session, identifies what is worth persisting, and presents a filtered list for the engineer to review
- Claude drafts the changes and shows them for approval before writing anything
- Only after explicit confirmation does Claude write to the spec

Claude never writes to the spec without explicit engineer approval.


## Setup

### 1. Add `CLAUDE.md` to your spec repository

Copy `CLAUDE.md` from this folder to the root of your spec repository and adjust it to match your actual spec structure and any conventions your team follows.


### 2. Add the `/consolidate` skill to your code repository

Initially i was planning to add the consolidate sill as part of the spec repository, since additionalDirectories should load it automatically when running Claude Code on a code repo, but thers an [open issue](https://github.com/anthropics/claude-code/issues/30064) on Claude Code GitHub about it not working, until its fixed the recommended approach is to add the skill on every code repository you integrate with the spec.

So copy the `skills/consolidate/` folder from this directory to `.claude/skills/` in your code repository:

```
code-repository/
└── .claude/
    └── skills/
        └── consolidate/
            └── SKILL.md
```


### 3. Add or edit `settings.json` in each code repository

Create or edit `.claude/settings.json` in each code repository with the spec repository listed as an additional directory:

```json
{
  "permissions": {
    "additionalDirectories": ["~/specs/{project-name}"]
  }
}
```

This makes the spec repository, available in every Claude Code session running in that repository. Commit this file so the configuration is shared across the team.


### 4. Add a spec section to each code repository's `CLAUDE.md`

If the repository does not have a `CLAUDE.md` yet, generate one first:

```
claude init
```

Then add the following section to the file:

```markdown
## Spec

The spec for this project is available on `~/specs/cefis`.
It is the single source of truth for business rules, use cases, and domain knowledge.

### Before starting any task
Always read the following before writing any code or making any decision:
1. `overview.md` — product vision and target users
2. `domain.md` — shared vocabulary and domain concepts

### Before implementing a feature
Identify which module the feature belongs to, then read:
- `modules/{module}/overview.md` — module context and boundaries
- `modules/{module}/use-cases/` — existing use cases for this module
- `modules/{module}/rules.md` — business rules for this module

### Never
- Contradict or ignore any rule or use case in the spec without explicit engineer confirmation
- Write to the spec directly — use /consolidate at the end of the session instead
```

> One approach to prevent every team member having to place the specs on the exact same absolute path is to use relative paths like `../spec` on both the `additionalDirectories` and `CLAUDE.md`.
