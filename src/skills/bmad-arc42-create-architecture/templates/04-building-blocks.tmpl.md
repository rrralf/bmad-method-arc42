# Building Block View

> arc42 §5 — Static decomposition of the system into building blocks
> with their responsibilities, interfaces, and contracts.
>
> **Levels:** Level 1 = major blocks (system floor plan). Level 2 = zoom into important blocks.
> **Contracts:** Each block defines what it *exposes* (published interface) and what it *consumes* (required input). Blocks don't know who consumes them — they define their shape, like Lego bricks.
> **DDD note:** Level 1 blocks often align with bounded contexts, but building blocks are about *static decomposition*, not *semantic boundaries*. Don't force DDD terminology if it doesn't fit.

---

## Level 1: System Decomposition

### Overview Diagram (C4 Level 2)

```
<!-- C4 Container diagram: system → major blocks → external systems -->
```

### Block Overview

| Block | Responsibility | Technology |
|-------|---------------|------------|

---

## Level 1 Block Details

<!-- Repeat this canvas for each Level 1 block -->

### Block: {{block_name}}

| Field | Value |
|---|---|
| **Responsibility** | {{one sentence}} |
| **Boundaries** | IN: {{what enters}}. OUT: {{what leaves}}. NOT: {{what this block does NOT do}} |
| **Technology** | {{languages, frameworks, services}} |
| **NFR overrides** | {{block-specific quality requirements, if different from system-level}} |
| **Risks** | {{what can go wrong in this block}} |
| **Key decisions** | → [ADR-xxx](../adr/xxx.md) |

#### Exposes (published contracts)

| Contract | Type | Schema | Description |
|----------|------|--------|-------------|

#### Consumes (required inputs)

| Contract | Type | From | Description |
|----------|------|------|-------------|

---

## Level 2: {{block_name}} — Internal Structure

<!-- Repeat for each block that needs deeper documentation (complex, risky, novel) -->

### Components

| Component | Responsibility | In | Out |
|-----------|---------------|-----|-----|

### Domain Model (within this block)

| Entity | Type | Key Fields | Lifecycle |
|--------|------|------------|-----------|
