# Step 1b: Continue Existing Workflow

## YOUR TASK:

Resume an existing arc42 architecture workflow from where it left off.

## CONTINUATION SEQUENCE:

### 1. Read Current State

Read `{architecture_output}/README.md` frontmatter:
- `stepsCompleted` — which steps are done
- `features` — which features were detected
- `inputDocuments` — which documents were loaded

### 2. Determine Next Step

Find the first incomplete step and report:

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

Load the step file corresponding to the next incomplete step.
