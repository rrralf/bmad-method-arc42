# Step 1b: Continue Existing Workflow

## YOUR TASK:

Resume an existing arc42 architecture workflow from where it left off.

## CONTINUATION SEQUENCE:

### 1. Read Current State

Read `{architecture_output}/README.md` frontmatter:
- `stepsCompleted` — which steps are done
- `stepsSkipped` — which steps were excluded by flags or topology
- `interaction_mode` — `discovery` or `review` (see INTERACTION MODES in `../workflow.md`)
- `execution_topology` — which variant of the quality sections applies
- `decision_source` — whether decisions are owned elsewhere
- `features` — which features were detected
- `inputDocuments` — which documents were loaded

Carry all of these forward. Re-deriving them mid-workflow produces a document whose halves
were written under different assumptions.

### 2. Determine Next Step

Find the lowest step number in neither `stepsCompleted` nor `stepsSkipped` and report:

"Welcome back {{user_name}}! Resuming arc42 architecture for {{project_name}}.

**Completed:** Steps {stepsCompleted}
**Next:** Step {next_step_number} — {next_step_description}

**Documents generated so far:**
{list of existing files in architecture_output}

[C] Continue to step {next_step_number}
[R] Restart from scratch (will overwrite existing docs)"

### 3. Handle User Choice

- **[C]** → Load the appropriate step file
- **[R]** → Confirm destructive action, then restart from step-01-init.md fresh workflow

## NEXT STEP:

Load the step file for the lowest step number that is in neither `stepsCompleted` nor `stepsSkipped`.
