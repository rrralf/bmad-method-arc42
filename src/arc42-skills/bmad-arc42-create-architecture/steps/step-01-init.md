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
- `{planning_artifacts}/**` — resolved from `_bmad/arc42/config.yaml`; if `_bmad/bmm/config.yaml`
  exists and sets a different value, prefer bmm's (the project already stores artifacts there)
- `{output_folder}/**`
- `{project-root}/docs/**`

If `{planning_artifacts}` resolves to a path that does not exist, say so rather than searching
on silently. An empty result from an unconfigured path looks exactly like a project with no
planning documents, and that difference decides whether step 3 refuses to continue.

Look for:
- Product Brief (`*brief*.md`)
- PRD (`*prd*.md`)
- Product Strategy (`*strategy*.md`)
- UX Design (`*ux-design*.md`)
- Research Documents (`*research*.md`)
- Project Context (`**/project-context.md`)
- Existing architecture docs (`{architecture_output}/**`)

**Loading Rules:**
- Load ALL discovered files completely
- Track in frontmatter `inputDocuments` array
- Confirm findings with user before proceeding

### 2b. Where Do Decisions Already Live?

Before writing anything, establish whether this package is the origin of architectural
decisions or a derived view of them. Ask:

"Do architectural decisions already live somewhere — a spec with a rationale log, an RFC
folder, a decision journal, a wiki? If so, that stays the source of truth and I'll link to
it instead of restating it here."

Record in frontmatter:

```yaml
decision_source: 'none' # or a path/URL — e.g. 'des-specs/decisions/' or a Confluence space
```

If a source exists, state the consequence plainly so it isn't a surprise at step 8:
"Then I won't duplicate those decisions. I'll write ADRs only for decisions that have no
home yet, and index the existing ones as links. Two descriptions of one system drift, and
then nobody knows which the code follows."

### 2c. Choose Interaction Mode

Judge how much is already decided and written down. This sets the shape of every later
step — see INTERACTION MODES in `../workflow.md`.

- Inputs are a brief and little else, decisions still open → `discovery`
- A PRD, spec or decision log covers most of the ground → `review`

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

### 3. Validate Required Inputs

**PRD or Product Strategy required.** At least one must exist.
- If neither found: "Architecture requires a PRD or Product Strategy. Please provide one."
- Do NOT proceed without at least one.

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
- PRD: {status}
- Strategy: {status}
- UX Design: {status}
- Research: {status}
- Existing arch docs: {status}

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

After user selects [C], update frontmatter `stepsCompleted: [1]`, then load `./step-02-context.md`.
