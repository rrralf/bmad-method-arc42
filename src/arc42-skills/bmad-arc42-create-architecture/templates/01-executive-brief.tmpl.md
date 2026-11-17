# {{project_name}} — Executive Brief

> arc42 §1 Introduction & Goals · §3 Context & Scope · §4 Solution Strategy

## What is {{project_name}}?

{{system_description}}

## Key Stakeholders

| Stakeholder | Concern | Influence |
|-------------|---------|-----------|

## System Context (C4 Level 1)

```
<!-- C4 Context diagram: actors → system → external systems -->
```

## Quality Goals

| Priority | Quality | Scenario |
|----------|---------|----------|

## What Shapes This System

> The circumstances we did **not** choose, and what follows from them. For a reader
> arriving in a year this is worth more than the list of decisions: it explains how
> little freedom there was, and which decisions were forced rather than preferred.

### Given (not chosen)

| Circumstance | Where it comes from | What it forecloses |
|--------------|--------------------|--------------------|
| {{external_given}} | {{origin — regulation, platform, budget, existing system}} | {{options it takes off the table}} |

### Follows from the above

<!-- Decision column: link to whoever owns the decision — a local ADR
     ([ADR-001](../adr/001-slug.md)) or, when it lives in a `decision_source`, the source
     itself, marked ↗ ([↗ AD-3](../../planning/ARCHITECTURE-SPINE.md#ad-3--…)). Never create a
     local ADR just to have something to link to. -->
| Decision | Derived from | Owner |
|----------|--------------|-------|
| {{decision}} | {{which given(s)}} | {{[ADR-NNN](../adr/NNN-slug.md) or [↗ source-id](link)}} |

## Solution Strategy

> Decisions we were genuinely free to make. If a row here is really forced by a
> circumstance above, move it — the distinction between chosen and imposed is the
> point of splitting these two sections.

| Decision | Approach | Rationale | Owner |
|----------|----------|-----------|-----|
