# bmad-method-arc42

> arc42-lite architecture documentation workflow for [BMAD](https://github.com/bmad-code-org/bmad)

Generates **multi-file** architecture documentation following the [arc42](https://arc42.org/) template, combined with [4+1 View Model](https://en.wikipedia.org/wiki/4%2B1_architectural_view_model) and [C4 Model](https://c4model.com/) diagram conventions.

## Why?

The default BMAD architecture workflow generates a single markdown file. This module generates a **proper documentation structure** — one concern per file, with ADRs, diagrams, and arc42 section mapping.

## What it generates

```
docs/architecture/
├── README.md                    ← arc42 mapping + navigation
├── 1-architecture/
│   ├── 01-executive-brief.md    ← §1,3,4: context, goals, strategy
│   ├── 02-constraints-nfr.md    ← §2: NFRs, constraints
│   ├── 03-api-contract.yml      ← §6: API contract (if applicable)
│   ├── 04-logical-view.md       ← §5: building blocks
│   ├── 04-pipeline.md           ← §6: pipeline (if applicable)
│   ├── 05-services/             ← §6: per-service docs (if applicable)
│   ├── 06-deployment.md         ← §7: deployment view (if applicable)
│   └── 07-security.md           ← §8: cross-cutting concerns
├── 2-development/
│   ├── packages.md              ← workspace structure
│   └── patterns.md              ← conventions
├── 3-quality/
│   └── qa-strategy.md           ← §10: testing approach
├── adr/                         ← §9: architecture decision records
│   └── 001-*.md
└── diagrams/
    └── *.puml
```

## Features

- **11-step guided workflow** — each step produces 1-2 files through collaborative discovery
- **Feature detection** — skips sections not relevant to your project (no API? no api-contract.yml)
- **ADR generation** — collects decisions from all steps, generates formal ADRs
- **Resume support** — workflow state saved in README.md frontmatter, pick up where you left off
- **Configurable output** — default `docs/architecture/`, override per project

## Install

```bash
bmad install bmad-method-arc42
```

## Usage

Via Winston (Architect agent):
```
[A42] Create Architecture (arc42)
```

Or directly:
```
/bmad-create-architecture-arc42
```

## Configuration

Default config in `config.yaml`:

```yaml
architecture_output: docs/architecture
```

Override per project in `_bmad/arc42/config.yaml`.

## License

MIT
