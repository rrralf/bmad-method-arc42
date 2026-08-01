# Step 5: Runtime View — Pipeline, API, Services

## MANDATORY EXECUTION RULES:

- 📖 Read complete step file before acting
- 🛑 Do NOT generate content without user input
- ⚙️ CHECK FEATURES: Only generate sections where feature flag is true
- 📜 API-FIRST: if `has_api`, the OpenAPI contract is a REQUIRED deliverable — never optional, never "described in prose instead"
- ✅ Communicate in {communication_language}, write output in {document_output_language}

## OUTPUTS (conditional):

- `{architecture_output}/1-architecture/04-pipeline.md` — if `has_pipeline`
- `{architecture_output}/1-architecture/03-api-contract.yml` — **mandatory** if `has_api`
- `{architecture_output}/1-architecture/05-services/{name}.md` — if `has_services`

## YOUR TASK:

Document runtime behavior — how the system actually works at runtime. Arc42 §6.

## FEATURE-CONDITIONAL EXECUTION:

### If has_pipeline:

1. "Walk me through the pipeline — what triggers it, what stages, what's the output?"
2. "What happens when a stage fails?"
   - `server` / `hybrid`: "Retry? Skip? Alert?"
   - `local-process` / `browser`: "With no network in the path, what's actually transient?
     If nothing, the question is what the user gets *instead* — partial result, skipped
     row, refusal with an explanation?"
3. "What's the data shape at each stage boundary?"

Generate `04-pipeline.md` using template `./templates/04-pipeline.tmpl.md`, plus pipeline diagram.

### If has_api: (API-FIRST — mandatory artifact)

This project is **API-first**: the contract is the primary artifact, written *before*
the implementation, and the implementation conforms to it. A machine-readable
`03-api-contract.yml` therefore ships with every architecture package that has an API.
It is not a summary of existing code and not replaceable by prose.

1. "What API does the system expose? REST, GraphQL, gRPC?"
2. "Key endpoints — what are the main operations?"
3. "Authentication method?"
4. "What's the error shape? Uniform problem details, or per-endpoint?"
5. "Versioning — URL path, header, or none yet?"

**If REST:** generate `03-api-contract.yml` using template `./templates/03-api-contract.tmpl.yml`.
Repeat the `paths` entry per endpoint and the `components.schemas` entry per model —
the template shows one of each as the pattern. Keep it a skeleton: operations,
status codes and the shape of request/response bodies. Exhaustive field-level
schemas belong in code, not here.

**If GraphQL/gRPC:** the machine-readable contract is still mandatory — emit the SDL or
`.proto` as `03-api-contract.graphql` / `03-api-contract.proto`, and record the deviation
from `.yml` in the README navigation table.

Every endpoint listed in a block's **Exposes** table in `04-building-blocks.md` must
appear in the contract. If something is missing, ask — do not silently drop it.

Auth must match what step 7 will document in `07-security.md` — if the user names an
auth method here, carry it forward.

If the user resists writing the contract now ("we'll do it later", "the code already
has it"), state plainly that this breaks the API-first rule and leaves the package
incomplete, then generate a skeleton with the endpoints known so far and mark unknown
schemas as `TODO`. A skeleton with gaps beats a missing contract.

### If has_services:

1. "List each distinct service/component that deserves its own doc."
2. For each: "Purpose? Technology? Interfaces? Config?"

Generate `05-services/{name}.md` for each service using template `./templates/service.tmpl.md`.

### If no features enabled:

"No runtime-specific docs needed based on your feature flags. Moving on."

## NEXT STEP:

After approval, update frontmatter, then:
- If `has_deployment` → load `./step-06-deployment.md`
- If not → skip to `./step-07-crosscutting.md`
