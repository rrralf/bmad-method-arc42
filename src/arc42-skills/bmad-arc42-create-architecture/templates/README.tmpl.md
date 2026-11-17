---
stepsCompleted: [] # steps that ran and were approved
stepsSkipped: [] # steps excluded by feature flags or topology — never also in stepsCompleted
interaction_mode: '' # discovery (ask) | review (extract from inputs, confirm)
execution_topology: '' # server | hybrid | local-process | browser
features:
  has_api: false
  has_pipeline: false
  has_services: false
  has_deployment: false
inputDocuments: []
decision_source: [] # paths/URLs where decisions are already recorded; empty = this package originates them
workflowType: 'arc42-architecture'
project_name: '{{project_name}}'
user_name: '{{user_name}}' # omit this line when no user_name is configured
date: '{{date}}'
---

# Architecture Documentation

> **{{project_name}}** — {{system_description}}

## Source of Truth

<!-- Delete this section only if `decision_source` is empty — i.e. this package really is
     where the decisions originate. Otherwise it is the first thing a reader needs. -->

Architectural decisions for {{project_name}} are recorded in:

1. {{decision_source[0]}}
2. {{decision_source[1] — one line per source, in precedence order}}

This package is a *derived view*: it explains structure, and links to decisions rather than
restating them. **Where this package and a source disagree, the source wins; between
sources, the one listed first wins.**

ADRs under [`adr/`](adr/) cover only decisions that have no home there. Entries marked ↗ in
the decision index point outward and are not maintained here.

## arc42-lite Mapping

This documentation follows an **arc42-lite** structure — a pragmatic adaptation of the [arc42](https://arc42.org/) architecture template, combined with the [4+1 View Model](https://en.wikipedia.org/wiki/4%2B1_architectural_view_model) and [C4 Model](https://c4model.com/) diagram conventions.

| arc42 § | Section | Our Document |
|---------|---------|-------------|
| §1 Introduction & Goals | System context, actors, scope | [01-executive-brief](1-architecture/01-executive-brief.md) |
| §2 Constraints | NFRs, sizing, tech constraints | [02-constraints-nfr](1-architecture/02-constraints-nfr.md) |
| §3 Context & Scope | Merged with §1 | [01-executive-brief](1-architecture/01-executive-brief.md) |
| §4 Solution Strategy | Key approaches → ADR links | [01-executive-brief](1-architecture/01-executive-brief.md#solution-strategy) |
| §5 Building Blocks | Blocks, contracts, domain model | [04-building-blocks](1-architecture/04-building-blocks.md) |
| §6 Runtime View | API contract (mandatory when the system has an API), pipeline, services | [03-api-contract.yml](1-architecture/03-api-contract.yml), _rest generated per feature_ |
| §7 Deployment View | Infrastructure, environments | [06-deployment](1-architecture/06-deployment.md) |
| §8 Cross-cutting | Security, auth, observability | [07-security](1-architecture/07-security.md) |
| §9 Architecture Decisions | ADR registry | [adr/](adr/) |
| §10 Quality Requirements | Testing, CI gates | [qa-strategy](3-quality/qa-strategy.md) |
| — Development View | Packages, patterns (4+1) | [packages](2-development/packages.md), [patterns](2-development/patterns.md) |

## Quick Navigation

### 1. Architecture
| Document | Description |
|----------|-------------|
| [01-executive-brief.md](1-architecture/01-executive-brief.md) | System context, goals, actors, solution strategy |
| [02-constraints-nfr.md](1-architecture/02-constraints-nfr.md) | Non-functional requirements, sizing, tech constraints |
| [04-building-blocks.md](1-architecture/04-building-blocks.md) | Building blocks, published contracts, domain model |

### 2. Development
| Document | Description |
|----------|-------------|
| [packages.md](2-development/packages.md) | Workspace structure, package boundaries |
| [patterns.md](2-development/patterns.md) | Naming, structure, format conventions |

### 3. Quality
| Document | Description |
|----------|-------------|
| [qa-strategy.md](3-quality/qa-strategy.md) | Testing approach, CI quality gates |

### Decision Index

Every architectural decision, wherever it lives. Rows marked ↗ are owned elsewhere —
follow the link; they are not maintained in this package.

Statuses of ADRs written here: `Proposed` · `Accepted` · `Rejected` · `Deprecated` ·
`Superseded by ADR-NNN`. A ↗ row reports its owner's status; `— (not stated in source)`
means the owner gives none. The last column: ⏳ = accepted but not yet verified,
↻ = rejected with conditions that would reopen it.

| ADR | Title | Status | Confirmation / revisit |
|-----|-------|--------|------------------------|

### Diagrams
| Diagram | Description |
|---------|-------------|

## Deliberately Not Documented

> Sections absent from this package **by decision**, not by omission. Without this list a
> missing section reads as forgotten — and the difference between "this system has no API"
> and "we never got round to describing the API" is the whole point of writing it down.

| Section | Why it does not apply | Would change if |
|---------|----------------------|-----------------|
| {{section}} | {{why_not_applicable}} | {{what_would_bring_it_back}} |

## Principles

<!-- Keep the API-first line only if `has_api: true`. Without an API it is not a principle
     of this system, and stating it reads as a claim the package then fails to back. -->
- **API-first** — the OpenAPI contract is written before the implementation and ships as a
  mandatory part of this package; the code conforms to the contract, not the other way round
- **One concern per file** — each document has one reason to change
- **ADRs are immutable** — once accepted, create a new ADR to supersede
- **Code is truth** — docs explain *why*, not *what* (code does that){{; the API contract is
  the exception — there the document *is* the source of truth — only if has_api}}
- **arc42-lite** — use what helps, skip what doesn't
