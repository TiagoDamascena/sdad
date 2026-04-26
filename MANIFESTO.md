# The SDAD Manifesto

Spec-Driven Agentic Development is a set of principles for software teams that use AI agents as active participants in the development process.

As agents become increasingly capable of writing, reviewing, and refactoring code, the role of the software engineer shifts away from pure implementation and toward product direction, technical oversight, and decision-making. SDAD defines how humans and agents should work together to accelerate development without losing quality or building a product without direction.


## Principles

### The spec is the source of truth

A spec exists to capture what the software must do and why, not how it does it. It describes behavior and intent, independent of programming language, frameworks, database structures, or design patterns. It is written for both human and agent readers, and should be understandable without reading the code. If something is easily understood by reading the implementation, it does not belong in the spec.

### Spec and implementation are always in sync

The spec is not written once and forgotten. It evolves alongside the product. When implementation changes, the spec must reflect that change. When the spec changes, the implementation must follow. Outdated documentation is worse than no documentation, it misleads both humans and agents.

### Specs are implementation agnostic

A spec describes what the software must do, not how it does it. Implementation details like language, framework, database structure and design patterns do not belong in the spec. A good spec survives a full technology rewrite unchanged.

### Agents without a spec are unreliable

An agent operating without clear specification and context will fill the gaps with assumptions. Those assumptions may be locally coherent but globally wrong, producing code that works in isolation but diverges from the product's intent. A spec is not bureaucracy, it is the minimum context an agent needs to act predictably.

### Engineers decide and agents execute.

Every meaningful decision belongs to the engineer: what to build, which tradeoff to accept, which direction to take. Agents are capable executors, not decision-makers. Delegating judgment is not part of this standard.

### The engineer is always responsible

Using an agent does not transfer ownership. The engineer is responsible for the quality of what is built, its technical integrity, and its alignment with the product's goals. Agents are instruments, not co-owners.


## Why SDAD?

Many teams believe they are gaining speed by adopting AI in development. In practice, they are accelerating code delivery while review cycles grow longer, bugs and vulnerabilities multiply, rework increases, and technical debt accumulates. Engineers gradually understand less about how their own product works.

SDAD exists to give teams a principled foundation for extracting real value from agents in software development, not just moving faster but building better, with more confidence and less accumulated chaos over time.


## What SDAD is not

SDAD is not a development process. It is a philosophy. The process of how your team plans, specifies, implements, and reviews should be built around these principles, not prescribed by them. SDAD does not dictate a specific workflow, a file format for specs, or a preferred agent. Those decisions belong to the teams that adopt it.
