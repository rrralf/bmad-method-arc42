---
stepsCompleted: []
features:
  has_api: false
  has_pipeline: false
  has_services: false
  has_deployment: false
inputDocuments: []
workflowType: 'arc42-architecture'
project_name: '{{project_name}}'
user_name: '{{user_name}}'
date: '{{date}}'
---

# Architecture Documentation

> **{{project_name}}** — {{system_description}}

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

### Architecture Decision Records

Statuses: `Proposed` · `Accepted` · `Rejected` · `Deprecated` · `Superseded by ADR-NNN`.
The last column is derived from each ADR: ⏳ = accepted but not yet verified,
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

- **API-first** — the OpenAPI contract is written before the implementation and ships as a
  mandatory part of this package; the code conforms to the contract, not the other way round
- **One concern per file** — each document has one reason to change
- **ADRs are immutable** — once accepted, create a new ADR to supersede
- **Code is truth** — docs explain *why*, not *what* (code does that); the API contract is
  the exception — there the document *is* the source of truth
- **arc42-lite** — use what helps, skip what doesn't
