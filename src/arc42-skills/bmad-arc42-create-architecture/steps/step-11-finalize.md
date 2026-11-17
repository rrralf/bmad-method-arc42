# Step 11: Finalize — Update README & Summary

## MANDATORY EXECUTION RULES:

- 📖 Read complete step file before acting
- ✅ Communicate in {communication_language}

## YOUR TASK:

Update README.md with final navigation, verify all files exist, present summary.

## FINALIZATION SEQUENCE:

### 1. Inventory Check

List all generated files in `{architecture_output}/`:
- Verify each file exists and is non-empty
- Note any missing files (skipped due to features)

**Empty directories.** `adr/` and `diagrams/` are created up front and may legitimately end
up empty — every decision owned by `decision_source`, every diagram inline in the document
that uses it. An empty directory left as-is reads as "forgotten" and does not survive a git
commit anyway. For each one still empty, do both:
- delete it, **or** place a one-paragraph `README.md` in it saying why it is empty;
- add a row to *Deliberately Not Documented* — the same rule as any other absence.

**API-first gate.** If `has_api: true`, the machine-readable contract
(`1-architecture/03-api-contract.yml`, or the `.graphql`/`.proto` variant) MUST exist and
MUST contain at least one operation. If it is missing, empty, or has no `paths` entries:

"⚠️ The API contract is missing from the package. This project is API-first — the contract
is a mandatory artifact, not an optional one. I can generate it now from what we discussed
in step 5.

[G] Generate the contract now
[S] Ship the package incomplete (recorded as a gap in the summary)"

Never report the documentation as complete while this gate is unmet — if the user picks
[S], mark §6 as ⚠️ **incomplete** in the coverage table instead of ✅.

### 2. Update README.md

Rebuild the Quick Navigation section with actual generated documents:
- Update "1. Architecture" table with files that exist
- Update "2. Development" table
- Update "3. Quality" table
- Update the "Decision Index" table with all ADRs **and** all externally-owned decisions
  (↗ rows), deriving the last column from each ADR file: ⏳ + the pending check for an
  `Accepted` ADR whose Confirmation is not discharged, ↻ + the conditions for a `Rejected`
  one, ✅ otherwise
- Keep the "Source of Truth" section if `decision_source` lists anything, one line per
  source in precedence order, with the precedence line intact; delete it only when the
  list is empty and this package genuinely originates the decisions
- Update "Diagrams" table with all generated diagrams
- Fill "Deliberately Not Documented" — one row per section skipped by a feature flag **and**
  per section dropped by `execution_topology` (uptime targets, retry strategy, alerting
  thresholds and secret rotation all disappear for a local system), with *why it does not
  apply* and *what would bring it back*. Never leave this section empty when flags were
  false: an unexplained gap is indistinguishable from an oversight
- Remove placeholder rows for files that weren't generated
- Append `11` to `stepsCompleted`. Do **not** add skipped steps to it — they stay in
  `stepsSkipped`; together the two lists must cover 1–11 exactly once

### 3. Summary Report

"Architecture documentation complete for {{project_name}}!

**Files generated:**
{list all files with paths}

**ADRs recorded:**
{list ADR titles}

**Skipped sections (recorded in README → Deliberately Not Documented):**
{list sections skipped due to feature flags, with the reason each does not apply}

**Open confirmations:**
{list Accepted ADRs whose Confirmation is still ⏳, with what needs measuring — these
are the decisions the team owes evidence for}

**arc42 coverage:**
| § | Section | Status |
|---|---------|--------|
| §1 | Introduction & Goals | ✅ |
| §2 | Constraints | ✅ |
| §3 | Context & Scope | ✅ (merged with §1) |
| §4 | Solution Strategy | ✅ (merged with §1) |
| §5 | Building Blocks | ✅ |
| §6 | Runtime View | {✅ or ⏭️ skipped} |
| §7 | Deployment View | {✅ or ⏭️ skipped} |
| §8 | Cross-cutting | ✅ |
| §9 | Decisions (ADRs) | ✅ ({n} local ADRs, {m} indexed from sources) |
| §10 | Quality | ✅ |

**Next steps:**
- Review each document and refine as needed
- Add diagrams where placeholders exist
- Create new ADRs as decisions evolve
- Keep docs in sync with code — one concern per file, easy to update"

## SUCCESS METRICS:

✅ All generated files verified
✅ README.md navigation reflects actual content
✅ All frontmatter updated
✅ Summary presented to user
✅ Workflow complete

## ON COMPLETE

Run `{workflow.on_complete}` if it is non-empty (see *Customization* in `../workflow.md`).
