# bmad-method-arc42

> arc42 architecture documentation generator for [BMAD](https://github.com/bmad-code-org/bmad) —
> a Claude Code skill that turns your PRD, spec and decisions into a multi-file docs-as-code
> package with ADRs, C4 diagrams and an arc42 section map.

The default BMAD architecture workflow writes one markdown file. This module writes a
**documentation structure** following the [arc42](https://arc42.org/) template, combined with
the [4+1 View Model](https://en.wikipedia.org/wiki/4%2B1_architectural_view_model) and
[C4 Model](https://c4model.com/) diagram conventions — one file per concern, so each document
has one reason to change.

## Quick start

```bash
npx bmad-method install \
  --directory /path/to/your/project \
  --custom-source https://github.com/rrralf/bmad-method-arc42.git \
  --tools claude-code \
  --yes
```

Then, in Claude Code inside that project:

```
/bmad-arc42-create-architecture
```

Requires the BMAD installer **v6.10+**. `bmm` is not required. More options under
[Install](#install).

## What it generates

```
docs/architecture/
├── README.md                    ← arc42 mapping, decision index, navigation
├── 1-architecture/
│   ├── 01-executive-brief.md    ← §1,3,4: context, goals, solution strategy
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
    └── *.puml or *.mmd          ← PlantUML or Mermaid
```

Sections that do not apply are skipped — and the README says so, with the reason.

## Example output

An excerpt from a package generated for a browser-only CSV viewer (no server, no API).
Absent sections are listed explicitly, so "this system has no API" can't be mistaken for
"nobody got round to describing the API":

> ### Deliberately Not Documented
>
> | Section | Why it does not apply | Would change if |
> |---------|----------------------|-----------------|
> | §6 API contract (`03-api-contract.yml`) | `has_api: false` — exposes no API to external consumers; everything is in-process in one tab | A programmatic interface is introduced |
> | §7 Deployment view (step 6 skipped) | `has_deployment: false` — static page, no server part; no infrastructure we operate | A backend appears |
> | Availability / uptime / SLO | No service to be up; replaced by *Durability of Local State* | A shared backend is introduced |
> | Retry, backoff, circuit breakers | No network in the path after load (AD-1); failures are properties of the input | A network dependency is added |

## How it adapts to your project

- **Execution topology** — `server`, `hybrid`, `local-process` or `browser`. Six sections
  have a variant per topology: for a system without a server, questions about uptime and
  retries are not just unnecessary, they are wrong.
- **API-first** — if the system exposes an API, a machine-readable OpenAPI contract is a
  mandatory artifact, written before the implementation. The final step refuses to report
  the package as complete while it is missing.
- **Existing decision sources** — if decisions already live in a spec, an architecture spine
  or a decision log, the workflow indexes them by link instead of rewriting them as ADRs.
  Two descriptions of one system drift apart within weeks.
- **Discovery or review** — with thin inputs it works through the questions with you; with a
  complete PRD or spec it extracts a draft, marks where each statement came from, and asks
  only about what is genuinely missing.
- **Explicit absences** — every skipped section is listed under *Deliberately Not
  Documented*, marked either "by decision" or "consequence of …".
- **Reads BMAD 6.12 artifacts** — `SPEC.md`, `ARCHITECTURE-SPINE.md`, `DESIGN.md`,
  `EXPERIENCE.md`, `AGENTS.md` and their `.memlog.md` rationale logs, as well as a classic PRD.

## Features

- **11-step guided workflow** — each step produces 1–2 files and waits for your approval
- **ADR generation** — collects decisions from all steps and writes formal ADRs for those
  that have no home elsewhere
- **Resume support** — progress is kept in the README frontmatter (`stepsCompleted`,
  `stepsSkipped`); run the skill again to continue where you left off
- **Configurable output** — default `docs/architecture/`, override per project
- **Customizable** — standard BMAD `customize.toml`: persistent facts, extra activation
  steps, an `on_complete` action

## Install

> Tested on BMAD installer 6.10.0 and 6.12.4, standalone and alongside `bmm`. Earlier
> versions are unverified.

### From Git (recommended — no clone needed)

Fresh BMAD project — see [Quick start](#quick-start). A fresh non-interactive (`--yes`)
install needs `--tools` with a real IDE id; `npx bmad-method install --list-tools` lists them.

Add to / update an existing BMAD project:

```bash
npx bmad-method install \
  --directory /path/to/your/project \
  --custom-source https://github.com/rrralf/bmad-method-arc42.git \
  --action update \
  --yes
```

The installer re-clones the Git source on update, so re-running the command pulls the
latest version. Append `@<branch-or-tag>` to the URL to install something other than the
default branch.

### From a local clone (module development)

```bash
git clone https://github.com/rrralf/bmad-method-arc42.git

npx bmad-method install \
  --directory /path/to/your/project \
  --custom-source /path/to/bmad-method-arc42 \
  --action update \
  --yes
```

Point `--custom-source` at the **repo root**, not `src/`. The installer reads
`.claude-plugin/marketplace.json` and resolves the module from `src/arc42-skills/`.

The installer registers `arc42` as a module, copies it to `_bmad/arc42/` and configures the
Claude Code skill automatically — `/bmad-arc42-create-architecture` is available right after
install. The module declares its own `planning_artifacts`, so document discovery works
without `bmm`, and defers to bmm's value when bmm is present.

### Uninstall

```bash
rm -rf _bmad/arc42 .claude/skills/bmad-arc42-create-architecture
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

## Changelog

See [CHANGELOG.md](CHANGELOG.md).

## License

MIT
