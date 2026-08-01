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

Decisions **not** to do something count. "We considered X and chose not to" is an
architectural decision and deserves an ADR — otherwise it gets re-proposed every
quarter and re-argued from scratch. Ask explicitly: "What did we decide against?"

### 2. Generate ADRs

For each approved decision, generate an ADR using `./templates/adr.tmpl.md`:

- Number sequentially: 001, 002, ...
- Slug from title: `001-serverless-first.md`
- Fill context, decision, consequences, alternatives

**Status — use this vocabulary and no other:**

| Status | Means |
|--------|-------|
| `Proposed` | Option not chosen yet, still under discussion |
| `Accepted` | Decided; the code is expected to conform |
| `Rejected` | Decided NOT to do this |
| `Deprecated` | No longer applies, nothing replaced it |
| `Superseded by ADR-NNN` | Replaced by a later decision |

This is the Nygard/MADR vocabulary that ADR tooling understands. Do **not** invent
statuses such as "conditionally accepted" or "deferred" — conditionality is captured
by the two fields below instead, which keeps it visible without breaking the enum.

**Confirmation is mandatory for every `Accepted` ADR.** If the decision was made ahead
of measurement, record what will be checked, against what threshold, and when. If the
decision makes no measurable claim, write "Not applicable" and say why — an empty
Confirmation is a gap, an explicit "not applicable" is a decision.

**Revisit when is mandatory for every `Rejected` ADR.** A "no" with no revisit
conditions reads as permanent. Ask: "What would change our mind?"

Show each ADR for review before writing.

### 3. Update README

Add each ADR to the README.md's ADR table. The Confirmation column is derived, not
authored: an `Accepted` ADR whose Confirmation is still pending renders ⏳ — that's
how a decision made ahead of its evidence stays visible from the index.

```markdown
| [001](adr/001-serverless-first.md) | Serverless-First on AWS | Accepted | ✅ confirmed |
| [007](adr/007-in-memory-index.md)  | In-Memory Index         | Accepted | ⏳ pending — p95 < 200 ms, not yet measured |
| [022](adr/022-no-sync-backend.md)  | No Sync Backend         | Rejected | ↻ revisit: multi-device demand, or funded hosting |
```

## NEXT STEP:

After approval, update frontmatter, then load `./step-09-quality.md`.
