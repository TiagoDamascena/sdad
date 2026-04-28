# Spec

This repository is the single source of truth for the product. It captures what the product does, for whom, and the rules that govern its behavior, independent of how it is implemented.

It is read by both humans and AI agents, but the responsibility for keeping it accurate and up to date always belongs to the engineers.


## What belongs here

This spec covers product, what the software must do and why. It does not cover how it does it.

**Belongs here:**
- Business rules and constraints
- Use cases and user interactions
- Domain concepts and vocabulary
- User personas and profiles

**Does not belong here:**
- Implementation details like language, framework, database structure, design patterns
- Infrastructure and deployment


## Modules

A module represents a cohesive area of the product with clear boundaries, a set of features, rules, and concepts that naturally belong together. Good modules map to how the business thinks about the product, not how the code is structured.

When in doubt whether something deserves its own module, ask: could this area be explained independently to someone unfamiliar with the rest of the product? If yes, it is a module.


## Structure

```
spec/
├── README.md
├── overview.md          # What the product is, its purpose and business model
├── domain.md            # Shared vocabulary and concepts across the product
├── users.md             # User personas and profiles
├── modules/
│   └── {module}/
│       ├── overview.md  # What this module does and its boundaries
│       ├── domain.md    # Concepts specific to this module
│       ├── rules.md     # Business rules that govern this module
│       └── use-cases/
│           ├── index.md # List of all use cases in this module
│           └── {use-case}.md
├── assets/              # Images and other files used in the documentation
└── templates/           # Templates for new files
```


## Conventions

- File names in kebab-case: `auth-flow.md`, not `Auth Flow.md`
- Dates in ISO format: `YYYY-MM-DD`
- Keep each file focused, if a rules file is growing too large, that is a signal the module should be split
