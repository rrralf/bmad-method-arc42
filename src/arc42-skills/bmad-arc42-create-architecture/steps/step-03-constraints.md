# Step 3: Constraints & Non-Functional Requirements

## MANDATORY EXECUTION RULES:

- 📖 Read complete step file before acting
- 🛑 NEVER invent content. Check `interaction_mode` (see INTERACTION MODES in `../workflow.md`):
  in `discovery` ask the questions below; in `review` extract from the input documents,
  mark provenance, and ask only about what genuinely is not there
- ✅ Collaborate as a peer — propose, correct, refine together; an interviewer reads a
  script, a peer brings a draft
- ✅ Communicate in {communication_language}, write output in {document_output_language}

## OUTPUT:

`{architecture_output}/1-architecture/02-constraints-nfr.md`

## YOUR TASK:

Collaboratively define constraints and NFRs covering arc42 §2.

## DISCOVERY QUESTIONS:

### Technical Constraints
1. "Are there any hard technical constraints? (specific cloud provider, language, framework, existing systems to integrate with)"
2. "Budget constraints? Free tier only, limited spend, or flexible?"
3. "Team constraints? Solo dev, small team, specific skill sets?"

### Non-Functional Requirements

4. "Performance — any latency/throughput targets?"

**Questions 5 and 6 depend on `execution_topology`. Ask one variant, not both.**

If `server` / `hybrid`:
5. "Scalability — what's the expected load now vs. 12 months?"
6. "Availability — how bad is downtime? (hobby project vs. business critical)"

If `local-process` / `browser`:
5. "Nothing scales with users here — there's no shared instance. What grows instead?
   Usually it's the input: how large does it get, and where does the system stop coping?"
6. "Uptime doesn't apply without a service. The exposure is losing state the user thinks
   is saved — where does state live, and how can it disappear?"
   For `browser`, raise this explicitly even if the user doesn't: **the engine may evict
   storage under pressure.** That is documented platform behaviour, not an edge case, and
   it's the closest analogue to an availability risk this system has. Ask what the user
   loses when it happens and whether anything mitigates it (persistence request, export).

7. "Security — what data do we handle? Any compliance requirements?"

### Sizing

If `server` / `hybrid`:
8. "How much data do we process/store? Rough estimates."
9. "How many users/requests per day?"

If `local-process` / `browser`:
8. "How much data does one user's machine hold — inputs, saved state, caches?"
9. Skip request volume: with no shared instance there is nothing to count. Don't write a
   "Users / requests per day — not applicable" row either; the dropped question belongs in
   README → *Deliberately Not Documented* with the scalability variant.

## GENERATION:

Generate `02-constraints-nfr.md` using template. Show for review.

"Here are the Constraints & NFRs:

[show content]

[A] Approve and continue
[E] Edit"

## NEXT STEP:

After approval, append `3` to `stepsCompleted` (see *Step State* in `../workflow.md`), then load `./step-04-building-blocks.md`.
