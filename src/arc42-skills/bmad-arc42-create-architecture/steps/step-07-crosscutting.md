# Step 7: Cross-Cutting Concerns

## MANDATORY EXECUTION RULES:

- 📖 Read complete step file before acting
- 🛑 NEVER invent content. Check `interaction_mode` (see INTERACTION MODES in `../workflow.md`):
  in `discovery` ask the questions below; in `review` extract from the input documents,
  mark provenance, and ask only about what genuinely is not there
- ✅ Communicate in {communication_language}, write output in {document_output_language}

## OUTPUT:

`{architecture_output}/1-architecture/07-security.md`

## YOUR TASK:

Document cross-cutting concerns — security, observability, error handling, config management. Arc42 §8.

## DISCOVERY QUESTIONS:

Several of these have two variants selected by `execution_topology`. Ask the matching
one. **"Does not apply" is a valid and valuable answer** — record it with its reason and
a link to whatever states that reason — a local ADR, a ↗ decision source, or the input
section that says it — rather than leaving a blank. Don't create an ADR just to have
something to link to. An empty section is indistinguishable from an
unanswered question; an explicit absence is a documented decision.

### Security
1. "How do users authenticate? (API keys, OAuth, JWT — or none, because there's nothing
   to guard)"
2. "Authorization model? (RBAC, simple owner, public — or none)"
3. "Sensitive data? (PII, credentials, tokens) — how stored/transmitted?"

If the answer to 1 or 2 is "none", ask *why* and record that: "nothing shared to protect",
"runs entirely on the user's machine". That reason is the useful part.

### Observability

If `server` / `hybrid`:
4. "How do we know it's working? (logs, metrics, alerts)"
5. "Structured logging? What format?"
6. "Any monitoring/alerting tools?"

If `local-process` / `browser`:
4. "Does any telemetry leave the user's machine? If not — is that a deliberate policy?"
5. "When something goes wrong, what can the user see? Where does it surface?"
6. "If a user reports a problem, what can they capture and send you?"

Thresholds and alerts presuppose someone receiving them. Don't ask for them when there's
no recipient. If telemetry is forbidden by policy, that's a privacy commitment
constraining every future feature — capture it as an ADR candidate, not a footnote.

### Error Handling
7. "Error strategy — fail fast, retry, circuit breaker?"
   For `local-process` / `browser`: "with no network in the path, which failures are even
   transient? If none, what does the user get instead of a retry?"
8. "How do errors surface to the user?"

### Configuration
9. "Where does config live? (env vars, config files, parameter store)"
10. "Are there any secrets at all?" — only if yes: "how are they stored and rotated?"
    If no, record that no-secrets is a *consequence of the architecture*, not an oversight.

## GENERATION:

Generate `07-security.md` using template `./templates/07-security.tmpl.md`. Keep the
variant sections matching `execution_topology` and delete the others. Show for review.

## NEXT STEP:

After approval, append `7` to `stepsCompleted` (see *Step State* in `../workflow.md`), then load `./step-08-decisions.md`.
