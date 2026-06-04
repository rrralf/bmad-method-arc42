# Step 5: Runtime View — Pipeline, API, Services

## MANDATORY EXECUTION RULES:

- 📖 Read complete step file before acting
- 🛑 Do NOT generate content without user input
- ⚙️ CHECK FEATURES: Only generate sections where feature flag is true
- ✅ Communicate in {communication_language}, write output in {document_output_language}

## OUTPUTS (conditional):

- `{architecture_output}/1-architecture/04-pipeline.md` — if `has_pipeline`
- `{architecture_output}/1-architecture/03-api-contract.yml` — if `has_api`
- `{architecture_output}/1-architecture/05-services/{name}.md` — if `has_services`

## YOUR TASK:

Document runtime behavior — how the system actually works at runtime. Arc42 §6.

## FEATURE-CONDITIONAL EXECUTION:

### If has_pipeline:

1. "Walk me through the pipeline — what triggers it, what stages, what's the output?"
2. "What happens when a stage fails? Retry? Skip? Alert?"
3. "What's the data shape at each stage boundary?"

Generate `04-pipeline.md` + pipeline diagram.

### If has_api:

1. "What API does the system expose? REST, GraphQL, gRPC?"
2. "Key endpoints — what are the main operations?"
3. "Authentication method?"

Generate `03-api-contract.yml` (OpenAPI skeleton) or description doc.

### If has_services:

1. "List each distinct service/component that deserves its own doc."
2. For each: "Purpose? Technology? Interfaces? Config?"

Generate `05-services/{name}.md` for each service using service template.

### If no features enabled:

"No runtime-specific docs needed based on your feature flags. Moving on."

## NEXT STEP:

After approval, update frontmatter, then:
- If `has_deployment` → load `./step-06-deployment.md`
- If not → skip to `./step-07-crosscutting.md`
