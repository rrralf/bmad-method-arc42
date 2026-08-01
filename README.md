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
│   ├── 03-api-contract.yml      ← §6: OpenAPI contract (mandatory if the system has an API)
│   ├── 04-building-blocks.md    ← §5: building blocks, contracts, domain model
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
- **API-first** — if the system exposes an API, a machine-readable OpenAPI contract is a
  mandatory artifact of the package, written before the implementation. The final step
  refuses to report the docs as complete while it's missing
- **Feature detection** — skips sections not relevant to your project (no API? no api-contract.yml)
- **ADR generation** — collects decisions from all steps, generates formal ADRs
- **Resume support** — workflow state saved in README.md frontmatter, pick up where you left off
- **Configurable output** — default `docs/architecture/`, override per project

## Install

> **Requires BMAD installer v6.8+.** Use the `--custom-source` flag (a comma-separated
> list of Git URLs or local paths). The installer finds the module definition in `src/`
> automatically — no need to point at the subfolder. A **fresh** non-interactive
> (`--yes`) install also requires `--tools` with a real IDE id (e.g. `claude-code`);
> run `npx bmad-method install --list-tools` to see valid ids. Use `--directory` to
> target a project other than the current folder.

### Install directly from Git (recommended — no clone needed)

Fresh BMAD project:

```bash
npx bmad-method install \
  --directory /path/to/your/project \
  --custom-source https://github.com/rrralf/bmad-method-arc42.git \
  --tools claude-code \
  --yes
```

Add to / update an existing BMAD project:

```bash
npx bmad-method install \
  --directory /path/to/your/project \
  --custom-source https://github.com/rrralf/bmad-method-arc42.git \
  --action update \
  --yes
```

The installer re-clones the Git source on update, so re-running the command above
pulls the latest version.

### Install from a local clone (module development)

```bash
git clone https://github.com/rrralf/bmad-method-arc42.git

npx bmad-method install \
  --directory /path/to/your/project \
  --custom-source /path/to/bmad-method-arc42 \
  --action update \
  --yes
```

> Point `--custom-source` at the **repo root** (not `src/`). The installer reads
> `.claude-plugin/marketplace.json`, then resolves the module from
> `src/arc42-skills/` (where `module.yaml` + `module-help.csv` live next to the skill).

The installer registers `arc42` as a module, copies it to `_bmad/arc42/`, and
**configures the Claude Code skill automatically** (no manual wrapper needed) —
`/bmad-arc42-create-architecture` is available right after install.

### Uninstall

```bash
rm -rf _bmad/arc42 .claude/skills/bmad-arc42-create-architecture
```

## Usage

```
/bmad-arc42-create-architecture
```

## Configuration

The installer asks where architecture docs should live and writes the answer to
`_bmad/arc42/config.yaml` (the prompt and its default come from `src/arc42-skills/module.yaml`):

```yaml
architecture_output: docs/architecture
```

Edit that file to change the location for an existing project.

## License

MIT
