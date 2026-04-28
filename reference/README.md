# SDAD Reference Implementation

This directory contains a reference implementation of SDAD, one concrete way to apply the principles in the [manifesto](../MANIFESTO.md) in practice.

It is not the only way to implement SDAD. It is a starting point: a tested approach that teams can adopt as-is, adapt to their context, or use as inspiration to build their own.


## Who this is for

This implementation works best for small, high-ownership teams like startups, indie developers, or teams where the same people who write the code also define what the product does.

It assumes that engineers are close to the product decisions and can update the spec as part of their regular workflow. Organizations with a dedicated product team, separate PMs owning requirements, or strict change control processes will likely need a different approach.


## What this implementation covers

- **Spec structure:** how to organize and write specs that follow SDAD principles
- **Agent configuration:** how to instruct agents to read and respect the spec before acting
- **Bidirectional sync:** how to keep spec and implementation in sync, with the engineer always in control of changes


## Getting started

### 1. Create your spec repository

Copy the `spec/` folder from this directory, initialize a git repository inside it, and push it to your preferred git host.

```bash
cp -r spec/ ~/specs/{project-name}
cd ~/specs/{project-name}
git init
git add .
git commit -m "Initial commit"
```

> **Language:** write the spec in the language your team speaks. The spec is a communication tool first, so forcing a language that is not natural to the team creates friction and leads to a spec that no one maintains.

### 2. Open in Obsidian

The spec is a folder of markdown files with wikilinks for internal navigation. [Obsidian](https://obsidian.md) is the recommended tool for reading and editing it as a human, it renders wikilinks, allows graph visualization, and makes navigation between files natural.

Open the spec folder as a vault in Obsidian.

### 3. Fill in the root files

Start with the files at the root of the spec before creating any modules:

1. `overview.md` — what the product is, its purpose, and who it is for
2. `domain.md` — the vocabulary and concepts shared across the product
3. `users.md` — the personas and profiles of the people who use the product

Use the templates in `templates/` as a starting point for each file.

### 4. Create your first module

Once the root files are in place, identify the first meaningful area of your product and create a module for it:

```
modules/{module}/
├── overview.md
├── domain.md
├── rules.md
└── use-cases/
    └── index.md
```

Use the templates in `templates/` for each file. Start with `overview.md` to define the module's boundaries, then add rules and use cases as you go.


## Keeping spec and code in sync

The spec and the implementation must always reflect each other. This works in both directions.

**Before writing code**, the agent reads the relevant parts of the spec like the module overview, rules, and use cases to understand what the product must do before deciding how to do it.

**After a working session**, the engineer runs `/consolidate` to persist any new knowledge from the session into the spec. The agent reviews the session, identifies what is worth persisting, drafts the changes, and waits for the engineer's approval before writing anything.

The engineer is always responsible for both directions. The agent assists, it never acts without confirmation.

To enable this, follow the setup instructions for your agent:

- [Claude Code](./agents/claude/README.md)

Pull requests adding support for other agents are welcome.


## Creating the spec for an existing project

Filling a spec from scratch for a project that already exists can feel overwhelming. The good news is that most of the knowledge is already there, in the code, in the team's heads, and in past conversations.

### Root files

The root files, `overview.md`, `domain.md`, and `users.md`, capture core business knowledge that is hard to extract from code alone. The most effective way to fill them is through a conversation with an AI assistant: ask it to interview you about the product, one file at a time, and fill the templates based on your answers. This usually takes less than an hour and produces a solid first draft.

### Modules

Modules are where the code has the most to say. For each module, point an AI agent at the relevant code and ask it to analyze the implementation, identify use cases and business rules, clarify anything it got wrong or missed, than run `/consolidate` to store all the extracted knowledge on the spec.

This approach works best when the root files are already in place, a well-defined product overview and domain vocabulary help the agent understand what it is looking at.


## License

MIT, see [LICENSE](./LICENSE)

This implementation is based on [SDAD](../MANIFESTO.md). If you find it useful, consider crediting the original work — it helps the community grow.
