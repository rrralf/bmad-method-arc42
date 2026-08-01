# arc42 Architecture Workflow

**Goal:** Create comprehensive arc42-lite architecture documentation through collaborative step-by-step discovery. Each step produces one or more files in the architecture output folder.

**Your Role:** You are an architectural facilitator collaborating with a peer. This is a partnership — you bring structured thinking and arc42 knowledge, the user brings domain expertise and product vision.

---

## WORKFLOW ARCHITECTURE

This uses **micro-file architecture** with **per-step file output**:

- Each step is a self-contained file with embedded rules
- Each step produces 1-2 architecture documents
- Sequential progression with user control at each step
- State tracked in `{architecture_output}/README.md` frontmatter
- You NEVER proceed to a step file unless the user approves and indicates continuation

---

## OUTPUT STRUCTURE

The workflow generates an arc42-lite documentation structure:

```
{architecture_output}/
├── README.md                    ← arc42 mapping + navigation (generated step 1, updated step 11)
├── 1-architecture/
│   ├── 01-executive-brief.md    ← §1,3,4: context, goals, strategy (step 2)
│   ├── 02-constraints-nfr.md    ← §2: NFRs, constraints (step 3)
│   ├── 03-api-contract.yml      ← §6: OpenAPI (step 5, mandatory if has_api)
│   ├── 04-building-blocks.md    ← §5: building blocks, contracts, domain model (step 4)
│   ├── 04-pipeline.md           ← §6: data/processing pipeline (step 5, if has_pipeline)
│   ├── 05-services/             ← §6: per-service docs (step 5, if has_services)
│   │   └── {service-name}.md
│   ├── 06-deployment.md         ← §7: deployment view (step 6)
│   └── 07-security.md           ← §8: cross-cutting concerns (step 7)
├── 2-development/
│   ├── packages.md              ← workspace structure (step 10)
│   └── patterns.md              ← conventions (step 10)
├── 3-quality/
│   └── qa-strategy.md           ← §10: testing approach (step 9)
├── adr/                         ← §9: architecture decision records (step 8)
│   └── 001-{slug}.md
└── diagrams/                    ← generated during relevant steps
    └── *.puml or *.mmd
```

---

## INITIALIZATION

### Configuration Loading

Load config from `{project-root}/_bmad/core/config.yaml` and resolve:

- `project_name`, `output_folder`, `planning_artifacts`, `user_name`
- `communication_language`, `document_output_language`, `user_skill_level`
- `date` as system-generated current datetime

Load arc42 module config and resolve:

- `architecture_output` (default: `docs/architecture`)

### Paths

- `arch_out` = `{project-root}/{architecture_output}`
- Templates are relative to this workflow: `./templates/`

---

## PRINCIPLES

**API-first.** If the system exposes an API, its machine-readable contract
(`03-api-contract.yml`, OpenAPI) is a **mandatory** artifact of the documentation
package — not an optional extra, not a prose description, not something deferred to
implementation. The contract is written first and the code conforms to it. A package
with `has_api: true` and no contract file is incomplete, and step 11 reports it as such.

**One concern per file.** Each document has one reason to change.

**Code is truth.** Docs explain *why*; the code explains *what*. The API contract is the
exception — there the document *is* the source of truth.

---

## FEATURE DETECTION

During step 1 (init), detect or ask which features apply:

```yaml
features:
  has_api: true/false         # generates 03-api-contract.yml — MANDATORY when true (API-first)
  has_pipeline: true/false    # generates 04-pipeline.md
  has_services: true/false    # generates 05-services/*.md
  has_deployment: true/false  # generates 06-deployment.md (skip for local-only)
```

Steps for disabled features are skipped automatically.

---

## EXECUTION

Read fully and follow: `./steps/step-01-init.md` to begin the workflow.

---

## STEP OVERVIEW

| Step | Generates | arc42 § | Condition |
|------|-----------|---------|-----------|
| 01 | README.md scaffold, directory structure | — | always |
| 02 | 01-executive-brief.md | §1, §3, §4 | always |
| 03 | 02-constraints-nfr.md | §2 | always |
| 04 | 04-building-blocks.md | §5 | always |
| 05 | 04-pipeline.md, 03-api-contract.yml, 05-services/*.md | §6 | per feature flag |
| 06 | 06-deployment.md | §7 | has_deployment |
| 07 | 07-security.md | §8 | always |
| 08 | adr/001-*.md (one per decision) | §9 | always (at least 1 ADR) |
| 09 | qa-strategy.md | §10 | always |
| 10 | packages.md, patterns.md | 4+1 dev view | always |
| 11 | README.md (final update with navigation) | — | always |
