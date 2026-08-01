# Runtime View — Pipeline

> arc42 §6 Runtime View

## Pipeline Overview

```
<!-- Pipeline flow diagram -->
```

## Stages

| Stage | Input | Output | Trigger |
|-------|-------|--------|---------|

## Stage Details

### {{stage_name}}

**Input:** {{input}}
**Output:** {{output}}
**Processing:** {{processing_description}}
**Error handling:** {{error_handling}}

## Data Flow

```
<!-- End-to-end data flow with transformations -->
```

<!-- Two variants — keep the one matching `execution_topology`, delete the other. -->

## Retry & Error Strategy — variant: `server` / `hybrid`

| Failure | Retry | Fallback |
|---------|-------|----------|

## Failure Handling — variant: `local-process` / `browser`

> With no network in the path, failures aren't transient — retrying an unreadable file
> reads it again and fails again. Every failure is a property of the input, so the
> question isn't "how often do we retry" but "what does the user get instead".

| Failure | What it means about the input | What happens instead | Surfaced how |
|---------|------------------------------|---------------------|--------------|
| {{failure}} | {{malformed, unsupported, too large, missing field}} | {{skip row, partial result, refuse with explanation}} | {{message, log, marker in output}} |
