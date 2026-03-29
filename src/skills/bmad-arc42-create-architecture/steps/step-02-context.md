# Step 2: Executive Brief — Context, Goals & Strategy

## MANDATORY EXECUTION RULES:

- 📖 Read complete step file before acting
- 🛑 Do NOT generate content without user input
- ✅ Collaborate — ask questions, propose, refine together
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

### Solution Strategy (§4)
6. "What are the key technology choices already made? (language, framework, cloud, etc.)"
7. "What architectural approach? (monolith, microservices, serverless, event-driven...)"
8. "Why these choices? What alternatives were considered?"

For each strategic decision that emerges, note it — these become ADR candidates for step 8.

## GENERATION:

After discovery, generate `01-executive-brief.md` using template `./templates/01-executive-brief.tmpl.md`. Fill in all sections with the discovered content.

Show the generated content to the user for review:

"Here's the Executive Brief. Please review:

[show content]

[A] Approve and continue
[E] Edit — tell me what to change"

## NEXT STEP:

After approval, update README.md frontmatter `stepsCompleted: [1, 2]`, then load `./step-03-constraints.md`.
