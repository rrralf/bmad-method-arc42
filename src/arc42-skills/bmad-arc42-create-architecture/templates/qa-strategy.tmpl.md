# Quality Assurance Strategy

> arc42 §10 Quality Requirements

## Testing Approach

| Level | Scope | Tools | Coverage target |
|-------|-------|-------|----------------|

## Test Pyramid

```
        /  E2E  \        ← few, slow, high confidence
       /  Integ  \       ← moderate, API contracts
      /   Unit    \      ← many, fast, isolated
```

## CI Quality Gates

| Gate | Check | Blocks merge? |
|------|-------|--------------|

## Non-Functional Testing

| Quality | Test approach | Frequency |
|---------|--------------|-----------|

<!-- Two variants — keep the one matching `execution_topology`, delete the other. -->

## Environments — variant: `server` / `hybrid`

| Environment | Data | Purpose |
|-------------|------|---------|

## Test Inputs — variant: `local-process` / `browser`

> There are no environments to promote through: no shared instance, no database to seed, no
> accounts to fixture. What a test needs instead is an input, and the interesting inputs are
> the ones that break things.

| Input | What it exercises | Where it comes from |
|-------|------------------|--------------------|
| {{typical input}} | The happy path | {{sample file / fixture}} |
| {{malformed input}} | Failure handling — see the runtime view | {{fuzz corpus}} |
| {{input at the ceiling}} | The limit declared in Scale of Input | {{generated}} |

**Release verification:** {{how a build is checked before publishing, given there is no
staging tier}}
