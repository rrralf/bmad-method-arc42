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

### First install (new BMAD project)

```bash
# 1. Clone the module
git clone https://github.com/rrralf/bmad-method-arc42.git

# 2. Install BMAD with arc42 as custom content (point to src/)
npx bmad-method install \
  --custom-content /path/to/bmad-method-arc42/src \
  --tools none \
  --yes
```

### Add to existing BMAD project

```bash
# 1. Clone the module (if not already)
git clone https://github.com/rrralf/bmad-method-arc42.git

# 2. Update existing BMAD installation with arc42
npx bmad-method install \
  --custom-content /path/to/bmad-method-arc42/src \
  --action update \
  --tools none \
  --yes
```

### Update to latest version

```bash
# 1. Pull latest changes
cd /path/to/bmad-method-arc42 && git pull

# 2. Re-run installer
npx bmad-method install \
  --custom-content /path/to/bmad-method-arc42/src \
  --action update \
  --tools none \
  --yes
```

### Uninstall

Remove the module directory from your project:
```bash
rm -rf _bmad/arc42 _bmad/_config/custom/arc42
```

The installer registers `arc42` as a module and copies skills to `_bmad/arc42/`.

### Claude Code skill wrapper

After BMAD install, create a skill wrapper so `/bmad-arc42-create-architecture` works as a slash command:

```bash
mkdir -p .claude/skills/bmad-arc42-create-architecture
cat > .claude/skills/bmad-arc42-create-architecture/SKILL.md << 'EOF'
---
name: bmad-arc42-create-architecture
description: 'Create arc42-lite architecture documentation as multi-file structure with ADRs and diagrams. Use when the user says "create arc42 architecture" or "create architecture arc42" or "lets do arc42"'
---

Follow the instructions in _bmad/arc42/skills/bmad-arc42-create-architecture/workflow.md.
EOF
```

## Usage

Directly as a skill:
```
/bmad-arc42-create-architecture
```

## Configuration

Default config in `config.yaml`:

```yaml
architecture_output: docs/architecture
```

Override per project in `_bmad/arc42/config.yaml`.

## License

MIT
