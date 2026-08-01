# Changelog

All notable changes to this module are documented here.

The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

Because this module is a set of workflow instructions rather than executable code,
"changed behaviour" means what the workflow asks, generates, and refuses to skip.

## [0.2.0] — 2026-08-01

### Added

- **API-first contract.** New OpenAPI 3.1 template (`03-api-contract.tmpl.yml`) with
  RFC 9457 problem details as the uniform error shape. When `has_api` is set, the
  machine-readable contract is a **mandatory** artifact: step 5 will not substitute prose
  for it, and step 11 refuses to report the documentation complete while it is missing.
  GraphQL and gRPC systems emit SDL or `.proto` instead — still machine-readable, still
  mandatory.
- **`execution_topology`** (`server` | `hybrid` | `local-process` | `browser`), asked in
  step 1. Six sections now have two variants and the workflow keeps only the matching one:
  scalability becomes *scale of input*, availability becomes *durability of local state*
  (with storage eviction by the browser engine raised explicitly), retry strategy becomes
  *what happens instead*, observability drops thresholds and alerts in favour of what is
  visible locally, auth gains an explicit "absent by decision", and secrets are split out
  of configuration so rotation only appears once secrets exist.
- **`decision_source`.** If decisions already live in a spec or decision journal, that
  source stays authoritative. Step 8 writes ADRs only for decisions with no home yet and
  indexes the rest as ↗ links; README gains a *Source of Truth* section declaring
  precedence, and the ADR table becomes a *Decision Index* covering both origins.
- **`interaction_mode`** (`discovery` | `review`). In `review`, a step's questions become
  a checklist of what to extract from the input documents rather than a script to read
  aloud: it presents a filled draft with provenance markers (`[PRD §4.2]`, `[inferred]`,
  `[?]`) and asks only about what genuinely is not there. Confirmation is unchanged.
- **ADR `Confirmation` and `Revisit when` fields.** Confirmation is mandatory for every
  `Accepted` ADR — it records what will be measured and when, so a decision made ahead of
  its evidence stays visible. `Revisit when` is mandatory for every `Rejected` ADR.
  Both surface in the Decision Index as ⏳ and ↻.
- **README *Deliberately Not Documented* table.** Sections dropped by a feature flag or by
  topology are listed with why they do not apply and what would bring them back — the
  difference between "this system has no API" and "we never described the API".
- **Executive brief *What Shapes This System*.** Separates circumstances that were imposed
  from decisions that were genuinely free.
- **CHANGELOG.** This file.

### Changed

- ADR statuses are pinned to the Nygard/MADR vocabulary — `Proposed`, `Accepted`,
  `Rejected`, `Deprecated`, `Superseded by ADR-NNN` — and inventing statuses such as
  "conditionally accepted" is now explicitly forbidden. Conditionality lives in the two
  new fields, which keeps the enum readable by adr-tools and similar.
- Step 8 now requires asking what was decided *against*. Rejections get ADRs, not silence.
- The per-step rule `Do NOT generate content without user input` became
  `NEVER invent content` plus a mode check — the old wording pushed every step to
  interrogate users for what they had already written down.
- Steps 5 and 9 reference their templates, which existed but were never linked from the
  step files.
- Plugin manifest migrated to the Claude Code marketplace schema: relative `source` and
  `skills` paths, structured `owner`/`author`, plus homepage, license, category and
  keywords.

### Fixed

- The README template linked `04-logical-view.md` while the workflow generated
  `04-building-blocks.md`, so **every generated package contained dead links** in its
  arc42 mapping and navigation tables.
- The README documented configuration in a root `config.yaml` that has never existed;
  configuration lives in `_bmad/arc42/config.yaml`, populated by the installer from
  `module.yaml`.
- The workflow read `planning_artifacts` and `user_skill_level` from the core config, where
  neither exists — both are `bmm` keys, so on a project without bmm the step-1 discovery glob
  resolved to an undefined variable and found planning documents only if they happened to sit
  under `docs/`. The module now declares its own `planning_artifacts` and defers to bmm's
  value when bmm is installed; `user_skill_level` was unused and is gone.
- The step overview demanded "at least 1 ADR" from step 8, contradicting the origin split
  that legitimately yields zero local ADRs when `decision_source` owns every decision.
- Step 11 left `adr/` and `diagrams/` empty and unexplained when nothing landed in them —
  the exact ambiguity the *Deliberately Not Documented* table exists to remove, and empty
  directories do not survive a commit anyway.
- `qa-strategy.tmpl.md` still assumed dev/staging/prod environments — the same server-side
  assumption removed from six other sections. It now has a local-topology variant.

## [0.1.0] — 2026-03-29

Initial release, plus the adjustments made before versioning began.

### Added

- 11-step guided arc42-lite workflow generating a multi-file documentation structure with
  ADRs, C4 diagrams and arc42 section mapping.
- Feature detection (`has_api`, `has_pipeline`, `has_services`, `has_deployment`) so
  sections that do not apply are skipped.
- Resume support via `stepsCompleted` in the generated README frontmatter.
- BMAD module packaging for installer v6.8: `module.yaml` and `module-help.csv` alongside
  the skill in `src/arc42-skills/`, so `--custom-source` resolves the module without
  pointing at a subfolder.

### Changed

- Step 4 redesigned from a flat logical view into a Building Block View: a canvas per
  block (responsibility, boundaries, technology, NFR overrides, risks) and explicit
  *Exposes* / *Consumes* contract tables, so a block describes its own shape without
  knowing its consumers.
- The domain model moved out of a single top-level section into each block's Level 2,
  where the entities actually belong.

[0.2.0]: https://github.com/rrralf/bmad-method-arc42/compare/v0.1.0...v0.2.0
[0.1.0]: https://github.com/rrralf/bmad-method-arc42/releases/tag/v0.1.0
