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

Load core config from `{project-root}/_bmad/core/config.yaml` and resolve:

- `project_name`, `output_folder`, `user_name`
- `communication_language`, `document_output_language`
- `date` as system-generated current datetime

Load arc42 module config from `{project-root}/_bmad/arc42/config.yaml` and resolve:

- `architecture_output` (default: `docs/architecture`)
- `planning_artifacts` (default: `{output_folder}/planning-artifacts`)

**Do not read `planning_artifacts` from the core config — it is not there.** The key belongs
to the `bmm` module, so it exists only when bmm is installed, and then in
`_bmad/bmm/config.yaml`. This module declares its own copy in `module.yaml` precisely so the
workflow runs without bmm. If `_bmad/bmm/config.yaml` exists and disagrees, prefer bmm's
value: the project is already storing artifacts there.

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

**Never two descriptions of one system.** This package is not automatically the origin of
the decisions it describes. If the project already keeps decisions somewhere else — a spec
with a rationale log, an RFC folder, a decision journal — that place stays the source of
truth, and this package **links** to it rather than restating it. Copying a decision here
creates a second description that drifts within weeks, and then nobody knows which one the
code follows. Step 1 records where decisions live; step 8 writes ADRs only for decisions
that have no home yet, and indexes the rest.

**Code is truth.** Docs explain *why*; the code explains *what*. The API contract is the
exception — there the document *is* the source of truth.

---

## INTERACTION MODES

Every step runs in one of two modes, decided in step 1 and recorded in frontmatter as
`interaction_mode`. The rule that never changes: **never invent content.** What changes is
where the content comes from.

### `discovery` — inputs are thin

Decisions have not been made yet. Work through the step's questions conversationally, one
thread at a time, and let the answers shape the document. This is the default when the
inputs are a brief and little else.

### `review` — inputs are ready

Decisions are already made and written down — a PRD, a spec, a decision log. This is normal
when architecture follows planning rather than preceding it. **Do not interrogate the user
for what is already recorded.** Asking someone to re-state in chat what they wrote last week
is not collaboration; it wastes their time and invites them to answer carelessly or skip
the workflow.

Instead, for each step:

1. **Extract** the step's content from the input documents.
2. **Present a filled draft**, with every claim carrying its provenance:
   - `[PRD §4.2]` — taken from a document, cite where
   - `[inferred]` — derived by you from what's there; say from what
   - `[?]` — not in any input; this is a real question, and the only kind worth asking
3. **Ask for correction, not for dictation:**

   > "Here's what I extracted for {section}. Check the `[inferred]` rows especially — those
   > are mine, not yours. {n} items marked `[?]` aren't in any input and I need answers.
   >
   > [A] Approve · [E] Correct something · [Q] Answer the open questions"

Confirmation is still required — extraction is not authority, and an unreviewed draft is
just a plausible-looking guess. What's removed is the interrogation, not the review.

Drop the provenance markers when writing the final file; they belong to the conversation.
Keep `[?]` items that remain unanswered as explicit `TODO` lines in the document — an
unanswered question left visible is honest, one silently filled in is not.

### Switching

The mode is per-workflow but overridable per step. If a step's inputs turn out to be empty
in `review` mode, say so and fall back to questions for that step. If in `discovery` mode
the user says "it's all in the spec", switch to `review` and re-read.

---

## FEATURE DETECTION

During step 1 (init), detect or ask which features apply:

```yaml
execution_topology: server | hybrid | local-process | browser
features:
  has_api: true/false         # generates 03-api-contract.yml — MANDATORY when true (API-first)
  has_pipeline: true/false    # generates 04-pipeline.md
  has_services: true/false    # generates 05-services/*.md
  has_deployment: true/false  # generates 06-deployment.md (skip for local-only)
```

Steps for disabled features are skipped automatically.

### Execution Topology

Several arc42 sections silently assume the system runs on infrastructure we operate.
For a system that doesn't, those sections don't merely shrink — they ask the *wrong
question*, and filling them with dashes looks like sloppiness rather than a considered
absence. `execution_topology` picks which variant of each section is asked for:

| Value | Meaning |
|-------|---------|
| `server` | We operate the infrastructure it runs on |
| `hybrid` | Local client plus a backend we operate |
| `local-process` | Runs on the user's machine — CLI, desktop app, script |
| `browser` | Runs in the user's browser, no backend of ours |

| Section | `server` / `hybrid` | `local-process` / `browser` |
|---------|--------------------|-----------------------------|
| Scalability | Load: current vs target throughput | **Scale of input**: largest input, where it degrades |
| Availability | Uptime target, SLO, recovery | **Durability of local state** — for `browser`, the real risk is the engine evicting storage, not downtime |
| Retry strategy | Retry, backoff, circuit breaker for transient failures | **What happens instead** — with no network, failures are properties of the input, not transient |
| Observability | Logs, metrics, thresholds, alerts, tracing | What is observable locally, and where telemetry goes — often nowhere, by decision |
| Auth / authz | Mechanism, model, session handling | May be **absent by decision** — record it as such, with the ADR |
| Config & secrets | Sources, rotation, secret store | Config only; "no secrets" is a consequence of the architecture, not a gap |

The wrong-variant sections are not silently dropped — they land in the README's
**Deliberately Not Documented** table with the reason and what would bring them back.

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
| 08 | adr/001-*.md + Decision Index | §9 | always — but **zero** local ADRs is a valid outcome when `decision_source` owns every decision |
| 09 | qa-strategy.md | §10 | always |
| 10 | packages.md, patterns.md | 4+1 dev view | always |
| 11 | README.md (final update with navigation) | — | always |
