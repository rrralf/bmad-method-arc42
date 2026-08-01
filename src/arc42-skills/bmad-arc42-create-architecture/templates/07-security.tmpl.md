# Cross-Cutting Concerns

> arc42 §8 Cross-cutting Concepts

<!-- Several sections below come in two variants, selected by `execution_topology`.
     Keep the matching one and DELETE the other. Where a concern genuinely does not
     apply, do not leave the table empty — state the absence and its reason.
     "None, by decision, because X" is documentation. A blank table is an open question. -->

## Security

### Authentication

**Applies:** {{yes / no — by decision}}

{{auth_approach}}

<!-- If there is none, say so and give the reason:
     "None. The system runs entirely on the user's machine and holds no shared state or
     remote resource to guard — see ADR-xxx."
     A blank here invites the next reader to assume it was forgotten, and invites the
     author to invent a mechanism that does not exist. -->

### Authorization

**Applies:** {{yes / no — by decision}}

{{authz_approach}}

### Data Protection

| Data type | Classification | Protection |
|-----------|---------------|------------|

## Observability — variant: `server` / `hybrid`

### Logging
| What | Level | Where |
|------|-------|-------|

### Monitoring
| Metric | Threshold | Alert |
|--------|-----------|-------|

### Tracing
{{tracing_approach}}

## Observability — variant: `local-process` / `browser`

> There is no collector to send anything to, and often a deliberate policy against
> sending anything at all. Thresholds and alerts presuppose someone on the receiving end.
> What remains: what can a user — or a developer helping them — see when something goes
> wrong, on the machine where it went wrong?

**Telemetry leaving the machine:** {{none — by decision / opt-in / described below}}

<!-- If none: give the reason and link the ADR. This is a privacy commitment that
     constrains every future feature, not an empty section — say so plainly. -->

| Signal | Visible to whom | Where it surfaces | Retained |
|--------|----------------|-------------------|----------|
| {{errors, warnings, progress, counts}} | {{user / developer via console}} | {{UI, stderr, downloadable log}} | {{session only / until cleared}} |

**Diagnosing a reported problem:** {{what the user can capture and send, and how}}

## Error Handling

| Layer | Strategy | User impact |
|-------|----------|-------------|

## Configuration Management

### Configuration

| Config | Source | Default | Changed by |
|--------|--------|---------|-----------|

### Secrets

**Present:** {{yes / no}}

<!-- If none: "None. Nothing in this system authenticates to anything, so there is no
     credential to store or rotate — a consequence of the architecture, not a gap."
     Then delete the table. Rotation only means something once secrets exist. -->

| Secret | Store | Rotation | Rotated by |
|--------|-------|----------|-----------|
