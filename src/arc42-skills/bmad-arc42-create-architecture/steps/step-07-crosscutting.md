# Step 7: Cross-Cutting Concerns

## MANDATORY EXECUTION RULES:

- 📖 Read complete step file before acting
- 🛑 Do NOT generate content without user input
- ✅ Communicate in {communication_language}, write output in {document_output_language}

## OUTPUT:

`{architecture_output}/1-architecture/07-security.md`

## YOUR TASK:

Document cross-cutting concerns — security, observability, error handling, config management. Arc42 §8.

## DISCOVERY QUESTIONS:

### Security
1. "How do users authenticate? (API keys, OAuth, JWT, none)"
2. "Authorization model? (RBAC, simple owner, public)"
3. "Sensitive data? (PII, credentials, tokens) — how stored/transmitted?"

### Observability
4. "How do we know it's working? (logs, metrics, alerts)"
5. "Structured logging? What format?"
6. "Any monitoring/alerting tools?"

### Error Handling
7. "Error strategy — fail fast, retry, circuit breaker?"
8. "How do errors surface to the user?"

### Configuration
9. "Where does config live? (env vars, config files, parameter store)"
10. "Any secrets management? (AWS Secrets Manager, Vault, .env)"

## GENERATION:

Generate `07-security.md` using template. Show for review.

## NEXT STEP:

After approval, update frontmatter, then load `./step-08-decisions.md`.
