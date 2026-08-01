# ADR-{{number}}: {{title}}

**Status:** {{status}}
**Date:** {{date}}
**Deciders:** {{deciders}}
**Supersedes:** {{superseded_adr}}

<!--
Status vocabulary — use these five and nothing else. They are what adr-tools,
log4brains and the rest of the ADR tooling understand:

  Proposed              — option not chosen yet, still under discussion
  Accepted              — decided; the code is expected to conform
  Rejected              — decided NOT to do this (a real decision — record it)
  Deprecated            — no longer applies, nothing replaced it
  Superseded by ADR-NNN — replaced by a later decision

Do NOT invent statuses like "conditionally accepted" or "deferred". A decision
that is accepted but not yet verified is `Accepted` with an open Confirmation.
A decision still being weighed is `Proposed`. Conditionality belongs in the two
fields below, not in the status — that keeps the vocabulary machine-readable
while still making the condition visible in the ADR index.
-->

## Context

{{context}}

## Decision

{{decision}}

## Confirmation

> How do we know this decision holds — and when do we check?
> Required for every `Accepted` ADR. When a decision is made ahead of measurement,
> this is where the outstanding obligation is recorded; the ADR index in the README
> marks the decision ⏳ until it is discharged.

| Check | Threshold / expected result | When | State |
|-------|-----------------------------|------|-------|
| {{how_verified}} | {{threshold}} | {{when_checked}} | ⏳ pending |

<!-- If the decision makes no measurable claim (pure convention, naming, style),
     write "Not applicable — no measurable claim" plus one line saying why.
     An empty Confirmation is a gap; an explicit "not applicable" is a decision. -->

## Revisit when

> What would make us reopen this?
> Required for every `Rejected` ADR — a "no" without revisit conditions reads as
> permanent, and six months on nobody remembers it was contingent. Encouraged
> elsewhere: most decisions rest on assumptions that can expire.

- {{condition_1}}
- {{condition_2}}

## Consequences

### Positive
{{positive_consequences}}

### Negative
{{negative_consequences}}

### Risks
{{risks}}

## Alternatives Considered

| Alternative | Pros | Cons | Why rejected |
|-------------|------|------|-------------|
