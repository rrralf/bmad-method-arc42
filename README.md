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

> **Requires BMAD installer v6.10+.** Tested on 6.10.0 and 6.12.4 (standalone and alongside
> `bmm`). Earlier versions are unverified. Use the `--custom-source` flag (a
> comma-separated list of Git URLs or local paths); the installer reads
> `.claude-plugin/marketplace.json` and resolves the module from the `skills` paths listed
> there, which are relative to the repository root. A **fresh** non-interactive (`--yes`)
> install also requires `--tools` with a real IDE id (e.g. `claude-code`); run
> `npx bmad-method install --list-tools` to see valid ids. Use `--directory` to target a
> project other than the current folder, and `@<branch-or-tag>` after a Git URL to install
> from something other than the default branch.
>
> The module installs standalone — `bmm` is not required. It declares its own
> `planning_artifacts` so document discovery works either way, and defers to bmm's value
> when bmm is present.

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

The installer asks two questions (prompts and defaults in `src/arc42-skills/module.yaml`)
and writes the answers to `_bmad/config.toml` under `[modules.arc42]`:

```toml
[modules.arc42]
architecture_output = "{project-root}/docs/architecture"
planning_artifacts = "{project-root}/_bmad-output/planning-artifacts"
```

`_bmad/config.toml` is regenerated on every install. To change a value durably, re-run the
installer or pin it in `_bmad/custom/config.toml`. When `bmm` is installed, its
`planning_artifacts` takes precedence.

### Customization

Like the standard BMAD 6.12 skills, the workflow reads `customize.toml` through
`resolve_customization.py`. Override it in `_bmad/custom/bmad-arc42-create-architecture.toml`:

```toml
[workflow]
persistent_facts = [
  "We deploy only to AWS eu-central-1.",
  "file:{project-root}/docs/standards/*.md",
]
on_complete = "Open a PR with the generated docs."
```

`persistent_facts` are treated as settled decisions: the workflow cites them instead of
asking. `activation_steps_prepend` / `activation_steps_append` run before and after
configuration loading.

## License

MIT
