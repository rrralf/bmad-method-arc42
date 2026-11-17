# Step 8: Architecture Decision Records

## MANDATORY EXECUTION RULES:

- 📖 Read complete step file before acting
- 🛑 NEVER invent content. Check `interaction_mode` (see INTERACTION MODES in `../workflow.md`):
  in `discovery` ask the questions below; in `review` extract from the input documents,
  mark provenance, and ask only about what genuinely is not there
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

### 1b. Split by Origin — CHECK `decision_source` FIRST

If step 1 recorded any `decision_source`, sort the candidates into two piles before
writing anything:

| Pile | What happens |
|------|--------------|
| **Already recorded there** | **Do NOT write an ADR.** Index it: title, status, and a link into the source |
| **No home yet** | Write a full ADR here — this package becomes its origin |

Present the split for confirmation:

"These decisions are already recorded in {source} — I'll link to them rather than
restate them: {list}.

These have no home yet, so I'll write ADRs for them here: {list}.

Correct?"

Restating an externally-owned decision produces a second description of the same system.
It reads as harmless on the day it's written and is wrong within a month, because only one
of the two copies gets updated. If the user asks for a copy anyway, say this once, then do
as asked — but write the ADR body as a stub: title, status, one-sentence summary and a
prominent link, never the full rationale. A stub can go stale in only one way; a duplicate
rationale can contradict.

**Precedence.** State it in the ADR index, once: "Where this package and {sources} disagree,
the sources win, in the order listed." Without a declared winner, a future reader has two
plausible documents and no rule. With more than one source, the order recorded in step 1
is the order of precedence between them too.

**Status of an external decision** is whatever its source says, mapped onto the vocabulary
below when the mapping is unambiguous ("принято" → `Accepted`, "rejected" → `Rejected`).
When the source states no status, or one that doesn't map, write `— (not stated in source)`
— never pick `Accepted` on its behalf. The vocabulary governs ADRs written here; an index
row only reports what its owner says. A source status with a condition attached ("accepted
before measurement") maps to the plain status, and the condition goes into the last column
as ⏳ — the same way a local `Accepted` ADR with a pending Confirmation renders.

### 2. Generate ADRs

If the *No home yet* pile is empty, there is nothing to generate: say so in one line and go
to section 3. Zero local ADRs is a valid outcome when the sources own every decision.

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

Add every decision to the README.md's ADR table — both the ADRs written here and the ones
owned elsewhere. One table, so a reader sees the whole decision surface in one place; the
link target says who owns each entry, and ↗ marks the external ones.

The Confirmation column is derived, not authored: an `Accepted` ADR whose Confirmation is
still pending renders ⏳ — that's how a decision made ahead of its evidence stays visible
from the index. For external decisions, leave it blank unless the source states one.

```markdown
| [001](adr/001-serverless-first.md) | Serverless-First on AWS | Accepted | ✅ confirmed |
| [007](adr/007-in-memory-index.md)  | In-Memory Index         | Accepted | ⏳ pending — p95 < 200 ms, not yet measured |
| [022](adr/022-no-sync-backend.md)  | No Sync Backend         | Rejected | ↻ revisit: multi-device demand, or funded hosting |
| [↗ RFC-14](../../specs/decisions/rfc-014.md) | Event Envelope Format | Accepted | owned by specs/decisions |
```

If any row is external, put the precedence line directly above the table.

## NEXT STEP:

After approval, append `8` to `stepsCompleted` (see *Step State* in `../workflow.md`) — also when zero local ADRs were written, because the Decision Index was still built — then load `./step-09-quality.md`.
