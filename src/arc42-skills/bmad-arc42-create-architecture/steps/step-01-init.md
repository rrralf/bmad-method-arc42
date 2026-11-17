# Step 1: Initialize arc42 Architecture Workspace

## MANDATORY EXECUTION RULES (READ FIRST):

- 🛑 NEVER invent content — this step decides `interaction_mode` for all the others
- 📖 CRITICAL: Read complete step file before taking any action
- ✅ ALWAYS treat this as collaborative discovery between architectural peers
- 📋 YOU ARE A FACILITATOR, not a content generator
- ⚠️ ABSOLUTELY NO TIME ESTIMATES
- ✅ YOU MUST ALWAYS SPEAK OUTPUT in {communication_language}

## YOUR TASK:

Initialize the arc42 architecture workspace: detect existing state, discover inputs, create directory structure, detect features.

## INITIALIZATION SEQUENCE:

### 1. Check for Existing Workflow

Look for existing `{architecture_output}/README.md`:
- If exists and has frontmatter with `stepsCompleted` → load `./step-01b-continue.md`
- If not exists → fresh workflow (continue below)

### 2. Input Document Discovery

Discover and load context documents from:
- `{planning_artifacts}/**` — see *Configuration Loading* in `../workflow.md` for which
  module's value wins
- `{output_folder}/**` — includes `{output_folder}/specs/` where `bmad-spec` writes
- `{project-root}/docs/**`
- `{project-root}/AGENTS.md`, `{project-root}/CLAUDE.md` — repo conventions, if present

If `{planning_artifacts}` resolves to a path that does not exist, say so rather than searching
on silently. An empty result from an unconfigured path looks exactly like a project with no
planning documents, and that difference decides whether the next section refuses to continue.

Look for:

| Kind | Patterns | Produced by |
|------|----------|-------------|
| Spec | `**/SPEC.md` (+ its `.memlog.md`) | `bmad-spec` |
| PRD | `*prd*.md` | `bmad-prd` |
| Product Brief | `*brief*.md` | `bmad-product-brief` |
| Product Strategy | `*strategy*.md` | — |
| Architecture spine | `**/ARCHITECTURE-SPINE.md` (+ its `.memlog.md`), **or any document whose frontmatter says `type: architecture-spine`** — spines get renamed | `bmad-architecture` |
| UX | `**/DESIGN.md`, `**/EXPERIENCE.md`, `*ux-design*.md` | `bmad-ux` (older: `bmad-create-ux-design`) |
| Research | `*research*.md` | research skills |
| Project context | `**/project-context.md`, `AGENTS.md` | `bmad-project-context` |
| Existing architecture docs | `{architecture_output}/**` | this workflow |

A `.memlog.md` next to a spec or spine is its rationale log. Prefer it over re-deriving
rationale from the document, and never restate it — link to it.

**Loading Rules:**
- Load ALL discovered files completely
- Track in frontmatter `inputDocuments` array
- Confirm findings with user before proceeding

### 3. Validate Required Inputs — before asking anything else

**A PRD, a spec (`SPEC.md`) or a Product Strategy is required.** At least one must exist.
An architecture spine alone is not enough: it records decisions, not what the product is for.
- If none found: "Architecture requires a PRD, a spec or a product strategy. Please provide
  one — `bmad-prd` or `bmad-spec` can produce it."
- Do NOT proceed, and do not ask any of the questions below: they all presuppose a product.

### 3b. Where Do Decisions Already Live?

Before writing anything, establish whether this package is the origin of architectural
decisions or a derived view of them.

**Detect first, then ask.** These are decision sources by construction — propose them
without waiting to be told:
- an `ARCHITECTURE-SPINE.md` — its `AD-n` entries are decisions, its `.memlog.md` their rationale
- a document whose sections are a decision log (`AD-n`, `ADR-n`, `RFC-n`, "Decision:" blocks)
- a spec `.memlog.md` with `decision` entries

Then ask: "Do architectural decisions also live anywhere else — an RFC folder, a decision
journal, a wiki? Whatever already holds them stays the source of truth; I'll link to it
instead of restating it here."

Decisions may live in more than one place (a spine and a PRD section, say). Record every
source, **in order of precedence** — the first one wins over the later ones, and every
one of them wins over this package:

```yaml
decision_source: [] # e.g. ['docs/planning/ARCHITECTURE-SPINE.md', 'docs/planning/prd.md#5']
```

If a source exists, state the consequence plainly so it isn't a surprise at step 8:
"Then I won't duplicate those decisions. I'll write ADRs only for decisions that have no
home yet, and index the existing ones as links. Two descriptions of one system drift, and
then nobody knows which the code follows."

### 3c. Choose Interaction Mode

Judge how much is already decided and written down. This sets the shape of every later
step — see INTERACTION MODES in `../workflow.md`.

- Inputs are a brief and little else, decisions still open → `discovery`
- A PRD, spec, spine or decision log covers most of the ground → `review`

Architecture arriving *after* planning is the normal case, not the exception. When it does,
`review` is the right mode: the questions in later steps then serve as a **checklist of what
to extract**, not a script to read aloud. Making someone re-state in chat what they wrote
last week is not collaboration — it wastes their time and invites careless answers.

Say which mode you picked and why, and offer the switch:

"Your inputs look {complete / thin}, so I'll run in **{mode}** mode: {in review — I'll
extract each section from your documents and bring you a draft to correct, asking only
about what genuinely isn't there / in discovery — I'll work through the questions with you}.

[M] Switch mode"

Record in frontmatter:

```yaml
interaction_mode: review # or discovery
```

### 4. Feature Detection

Ask the user or infer from documents:

**First — where does the system actually execute?** This decides which *variant* of the
quality sections gets asked for later (scalability, availability, observability, auth,
config). Getting it wrong means asking about uptime for a system with no server.

- `server` — we operate the infrastructure it runs on
- `hybrid` — local client plus a backend we operate
- `local-process` — runs on the user's machine (CLI, desktop app, script)
- `browser` — runs in the user's browser, no backend of ours

"Based on what I've read, I'm detecting these architectural features:

- **API?** Does the system expose an API to external consumers? → `has_api`
  (this project is API-first — saying yes means a machine-readable `03-api-contract.yml`
  ships as a mandatory part of the documentation package)
- **Pipeline?** Is there a data processing pipeline or async workflow? → `has_pipeline`
- **Services?** Are there multiple distinct services/components to document separately? → `has_services`
- **Deployment?** Is there cloud/server infrastructure to document? → `has_deployment`

Please confirm or correct:"

```yaml
execution_topology: {{detected}}
features:
  has_api: {{detected}}
  has_pipeline: {{detected}}
  has_services: {{detected}}
  has_deployment: {{detected}}
```

### 5. Create Directory Structure

Create the workspace:

```
{architecture_output}/
├── README.md              ← from template, with frontmatter
├── 1-architecture/
│   └── (empty, populated by steps 2-7)
├── 2-development/
│   └── (empty, populated by step 10)
├── 3-quality/
│   └── (empty, populated by step 9)
├── adr/
│   └── (empty, populated by step 8)
└── diagrams/
    └── (empty, populated during relevant steps)
```

### 6. Report and Confirm

"Welcome {{user_name}}! I've set up your arc42 architecture workspace for {{project_name}}.

**Documents Found:**
- Spec / PRD / Strategy: {status}
- Architecture spine: {status}
- UX: {status}
- Research: {status}
- Project context: {status}
- Existing arch docs: {status}

**Decision sources** (in precedence order): {decision_source, or "none — this package originates them"}

**Execution topology:** {execution_topology}
_(quality sections will be asked in their {server-side / local} variant)_

**Features Detected:**
- API: {has_api}
- Pipeline: {has_pipeline}
- Services: {has_services}
- Deployment: {has_deployment}

**Steps planned:** {list only steps that apply based on features}

Ready to begin. Anything to add or correct?

[C] Continue to Executive Brief"

## SUCCESS METRICS:

✅ Existing workflow detected and handled
✅ Input documents discovered, loaded, confirmed
✅ Features detected and confirmed with user
✅ Directory structure created
✅ README.md scaffold written with frontmatter
✅ User confirmed and ready to proceed

## NEXT STEP:

After the user selects [C], append `1` to `stepsCompleted` (see *Step State* in `../workflow.md`), then load `./step-02-context.md`.
