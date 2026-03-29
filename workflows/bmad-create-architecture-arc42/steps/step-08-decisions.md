# Step 8: Architecture Decision Records

## MANDATORY EXECUTION RULES:

- 📖 Read complete step file before acting
- 🛑 Do NOT generate content without user input
- ✅ Communicate in {communication_language}, write output in {document_output_language}

## OUTPUT:

`{architecture_output}/adr/NNN-{slug}.md` — one file per decision

## YOUR TASK:

Create Architecture Decision Records for key decisions made during this workflow. Arc42 §9.

## PROCESS:

### 1. Collect Decision Candidates

Review all previous steps and collect decisions that were made:
- Technology choices from step 2 (Executive Brief → Solution Strategy)
- Constraint-driven decisions from step 3
- Structural decisions from step 4 (Building Blocks)
- Runtime decisions from step 5
- Deployment decisions from step 6
- Security decisions from step 7

Present the list:
"I've identified these architectural decisions from our conversation:

1. {decision_1}
2. {decision_2}
...

Which ones deserve a formal ADR? Any to add or remove?"

### 2. Generate ADRs

For each approved decision, generate an ADR using `./templates/adr.tmpl.md`:

- Number sequentially: 001, 002, ...
- Slug from title: `001-serverless-first.md`
- Status: `Accepted`
- Fill context, decision, consequences, alternatives

Show each ADR for review before writing.

### 3. Update README

Add each ADR to the README.md's ADR table:
```markdown
| [001](adr/001-serverless-first.md) | Serverless-First on AWS | Accepted |
```

## NEXT STEP:

After approval, update frontmatter, then load `./step-09-quality.md`.
