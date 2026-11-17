# Changelog

All notable changes to this module are documented here.

The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

Because this module is a set of workflow instructions rather than executable code,
"changed behaviour" means what the workflow asks, generates, and refuses to skip.

## [0.3.0] — 2026-11-17

BMAD 6.12 compatibility, and fixes for defects found by the first independent stand run
(an executor and a verifier that did not write the instructions).

### Added

- **Inputs produced by BMAD 6.12 skills.** Step 1 now discovers `SPEC.md` (`bmad-spec`),
  `ARCHITECTURE-SPINE.md` (`bmad-architecture`), `DESIGN.md` / `EXPERIENCE.md` (`bmad-ux`),
  `AGENTS.md` (`bmad-project-context`) and the `.memlog.md` rationale logs next to them.
  A spec now satisfies the input requirement — before, a project planned with `bmad-spec`
  alone was refused for lacking a PRD.
- **Decision sources are detected, not only asked about.** A spine's `AD-n` entries, a
  decision-log document or a spec memlog are proposed as `decision_source` automatically.
  A spine is recognised by its frontmatter (`type: architecture-spine`) as well as by file
  name, since spines get renamed.
- **`customize.toml`** with the standard BMAD fields: `persistent_facts` (treated as settled
  decisions, cited instead of asked), `activation_steps_prepend` / `_append`, `on_complete`.
- **`stepsSkipped`** in README frontmatter, alongside `stepsCompleted`.

### Changed

- **Configuration is read through `resolve_config.py`** (`_bmad/config.toml` plus
  `_bmad/custom/` overrides), with the per-module `config.yaml` files as a fallback.
- **`decision_source` is a list**, in precedence order. Decisions often live in more than
  one place (a spine and a PRD section); a single path forced the second owner into prose.
- **External decisions keep their owner's status.** When the source states none, the index
  says `— (not stated in source)` instead of the workflow choosing `Accepted` on its behalf.
- **Templates link decisions to their owner.** Executive brief, building blocks and
  security templates linked only to local `../adr/` files, which pushed toward duplicating
  externally-owned decisions; they now take a local ADR or a ↗ source link.
- **Absences say what kind they are**: "by decision" or "consequence of …". The security
  template labelled every absence "by decision", contradicting inputs that say otherwise.
- **One menu convention**: `[C]` for step 1, `[A]/[E]` (+ `[Q]` in review) for steps 2–10.
  Step files used three different menus, so "after approval" meant different things.
- **The Decision Index never ticks ✅ for an external decision.** Step 8 said leave the
  column blank, its example said "owned by …", step 11 said ✅ — three rules for one cell.
- **Input validation runs first** in step 1, before the questions about decision sources and
  interaction mode, which all presuppose a product.
- `module-help.csv`: phase `plan` (6.12 naming) instead of `3-solutioning`.

### Fixed

- `arch_out` was built as `{project-root}/{architecture_output}`, but the configured value
  already contains `{project-root}` — a doubled prefix.
- Step 11 wrote every step number into `stepsCompleted`, including steps skipped by a flag,
  so the frontmatter claimed work that was not done. Steps 4–10 said "update frontmatter"
  without saying to what. Every step now appends its own number to exactly one list.
- Step 3 asked "users/requests per day" regardless of topology; local and browser systems
  get a per-machine data question instead, and the dropped question goes to *Deliberately
  Not Documented*.
- The README template stated API-first as a principle even for systems without an API.
- Step 8 asked to show and generate ADRs when there were none to write.
- Step 11's coverage summary counted only local ADRs, reporting "0" for a package whose
  decisions are all indexed from a source.

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

[0.3.0]: https://github.com/rrralf/bmad-method-arc42/compare/v0.2.0...v0.3.0
[0.2.0]: https://github.com/rrralf/bmad-method-arc42/compare/v0.1.0...v0.2.0
[0.1.0]: https://github.com/rrralf/bmad-method-arc42/releases/tag/v0.1.0
