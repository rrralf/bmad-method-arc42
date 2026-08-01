# Step 10: Development View — Packages & Patterns

## MANDATORY EXECUTION RULES:

- 📖 Read complete step file before acting
- 🛑 NEVER invent content. Check `interaction_mode` (see INTERACTION MODES in `../workflow.md`):
  in `discovery` ask the questions below; in `review` extract from the input documents,
  mark provenance, and ask only about what genuinely is not there
- ✅ Communicate in {communication_language}, write output in {document_output_language}

## OUTPUTS:

- `{architecture_output}/2-development/packages.md`
- `{architecture_output}/2-development/patterns.md`

## YOUR TASK:

Document the development view — workspace structure, package boundaries, and coding conventions. 4+1 Development View.

## DISCOVERY — Packages:

1. "What's the workspace/repo structure? Monorepo? Multi-repo?"
2. "Key directories — what lives where?"
3. "Package/module boundaries — what depends on what?"
4. "Any hard dependency rules? (e.g., 'fetchers never import from output')"

## DISCOVERY — Patterns:

5. "Naming conventions? (files, functions, variables, classes)"
6. "Error handling pattern? (exceptions, Result types, error codes)"
7. "Configuration pattern? (env vars, config files, injection)"
8. "Commit conventions? (conventional commits, free-form)"

## GENERATION:

Generate both files. Show for review.

## NEXT STEP:

After approval, update frontmatter, then load `./step-11-finalize.md`.
