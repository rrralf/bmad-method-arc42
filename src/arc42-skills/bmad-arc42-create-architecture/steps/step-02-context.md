# Step 2: Executive Brief — Context, Goals & Strategy

## MANDATORY EXECUTION RULES:

- 📖 Read complete step file before acting
- 🛑 NEVER invent content. Check `interaction_mode` (see INTERACTION MODES in `../workflow.md`):
  in `discovery` ask the questions below; in `review` extract from the input documents,
  mark provenance, and ask only about what genuinely is not there
- ✅ Collaborate as a peer — propose, correct, refine together; an interviewer reads a
  script, a peer brings a draft
- ✅ Communicate in {communication_language}, write output in {document_output_language}

## OUTPUT:

`{architecture_output}/1-architecture/01-executive-brief.md`

## YOUR TASK:

Collaboratively create the Executive Brief covering arc42 §1 (Introduction & Goals), §3 (Context & Scope), and §4 (Solution Strategy).

## DISCOVERY QUESTIONS:

Work through these with the user. Don't dump all at once — conversational flow:

### System Context (§1, §3)
1. "In one paragraph — what does {{project_name}} do and why does it exist?"
2. "Who are the key actors/stakeholders? Who uses it, who operates it, who benefits?"
3. "What external systems does it interact with? APIs, databases, third-party services?"

### Quality Goals
4. "What are the top 3 quality attributes? (e.g., reliability, performance, maintainability, security)"
5. "For each — what does 'good enough' look like? Concrete scenarios."

### What Shapes This System
6. "Name up to three circumstances you did **not** choose but have to live with —
   regulation, platform limits, an existing system, budget, team size."
7. For each: "What options does it take off the table?"
8. "Which of our decisions follow directly from those, rather than from preference?"

This separates imposed from chosen. Keep the distinction in the generated document:
decisions forced by a circumstance go under *What Shapes This System*, genuinely free
ones under *Solution Strategy*. A reader a year from now needs to know which was which
— otherwise every constraint looks like it was up for debate.

### Solution Strategy (§4)
9. "What are the key technology choices genuinely open to you? (language, framework, cloud)"
10. "What architectural approach? (monolith, microservices, serverless, event-driven...)"
11. "Why these choices? What alternatives were considered — and what did you decide against?"

For each strategic decision that emerges, note it — these become ADR candidates for step 8.
Note decisions *against* something too: they get `Rejected` ADRs, not silence.

## GENERATION:

After discovery, generate `01-executive-brief.md` using template `./templates/01-executive-brief.tmpl.md`. Fill in all sections with the discovered content.

Show the generated content to the user for review:

"Here's the Executive Brief. Please review:

[show content]

[A] Approve and continue
[E] Edit — tell me what to change"

## NEXT STEP:

After approval, update README.md frontmatter `stepsCompleted: [1, 2]`, then load `./step-03-constraints.md`.
