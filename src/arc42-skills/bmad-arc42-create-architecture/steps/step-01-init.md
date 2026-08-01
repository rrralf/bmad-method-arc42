# Step 1: Initialize arc42 Architecture Workspace

## MANDATORY EXECUTION RULES (READ FIRST):

- 🛑 NEVER generate content without user input
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
- `{planning_artifacts}/**`
- `{output_folder}/**`
- `{project-root}/docs/**`

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

### 3. Validate Required Inputs

**PRD or Product Strategy required.** At least one must exist.
- If neither found: "Architecture requires a PRD or Product Strategy. Please provide one."
- Do NOT proceed without at least one.

### 4. Feature Detection

Ask the user or infer from documents:

"Based on what I've read, I'm detecting these architectural features:

- **API?** Does the system expose an API to external consumers? → `has_api`
  (this project is API-first — saying yes means a machine-readable `03-api-contract.yml`
  ships as a mandatory part of the documentation package)
- **Pipeline?** Is there a data processing pipeline or async workflow? → `has_pipeline`
- **Services?** Are there multiple distinct services/components to document separately? → `has_services`
- **Deployment?** Is there cloud/server infrastructure to document? → `has_deployment`

Please confirm or correct:"

```yaml
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
