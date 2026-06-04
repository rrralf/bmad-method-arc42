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

### 2. Update README.md

Rebuild the Quick Navigation section with actual generated documents:
- Update "1. Architecture" table with files that exist
- Update "2. Development" table
- Update "3. Quality" table
- Update "Architecture Decision Records" table with all ADRs
- Update "Diagrams" table with all generated diagrams
- Remove placeholder rows for files that weren't generated
- Update frontmatter: `stepsCompleted: [1,2,3,4,5,6,7,8,9,10,11]`

### 3. Summary Report

"Architecture documentation complete for {{project_name}}!

**Files generated:**
{list all files with paths}

**ADRs recorded:**
{list ADR titles}

**Skipped sections:**
{list sections skipped due to feature flags, if any}

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
| §9 | Decisions (ADRs) | ✅ ({n} ADRs) |
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
