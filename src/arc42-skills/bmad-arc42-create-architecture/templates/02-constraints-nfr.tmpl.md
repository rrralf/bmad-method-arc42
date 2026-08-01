# Constraints & Non-Functional Requirements

> arc42 §2 Constraints

## Technical Constraints

| Constraint | Description | Rationale |
|------------|-------------|-----------|

## Organizational Constraints

| Constraint | Description |
|------------|-------------|

## Non-Functional Requirements

### Performance

| Metric | Target | Measurement |
|--------|--------|-------------|

<!-- Scalability and Availability come in two variants. Keep the one matching
     `execution_topology` and DELETE the other — a section answering the wrong
     question is worse than an absent one. -->

### Scalability — variant: `server` / `hybrid`

| Dimension | Current | Target |
|-----------|---------|--------|

### Scale of Input — variant: `local-process` / `browser`

> Nothing here scales with users — there is no shared instance. What grows is the work
> a single run is handed.

| Dimension | Typical | Largest supported | Behaviour past that point |
|-----------|---------|-------------------|---------------------------|
| {{input_dimension}} | {{typical}} | {{ceiling}} | {{degrades / refuses / warns}} |

### Availability — variant: `server` / `hybrid`

| Requirement | Target |
|-------------|--------|

### Durability of Local State — variant: `local-process` / `browser`

> Uptime is meaningless without a service to be up. The real exposure is losing state
> the user believes is saved. For `browser`, the engine may evict storage under pressure
> — that is not an edge case, it is documented behaviour of the platform.

| State | Where it lives | How it can be lost | Mitigation | Consequence if lost |
|-------|---------------|--------------------|-----------|--------------------|
| {{what}} | {{IndexedDB / localStorage / file}} | {{eviction, clearing, uninstall, disk}} | {{persistence request, export, backup}} | {{what the user loses}} |

### Security

| Requirement | Approach |
|-------------|----------|

## Sizing Estimates

| Resource | Estimate | Basis |
|----------|----------|-------|
