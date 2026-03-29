# Step 3: Constraints & Non-Functional Requirements

## MANDATORY EXECUTION RULES:

- 📖 Read complete step file before acting
- 🛑 Do NOT generate content without user input
- ✅ Collaborate — ask questions, propose, refine together
- ✅ Communicate in {communication_language}, write output in {document_output_language}

## OUTPUT:

`{architecture_output}/1-architecture/02-constraints-nfr.md`

## YOUR TASK:

Collaboratively define constraints and NFRs covering arc42 §2.

## DISCOVERY QUESTIONS:

### Technical Constraints
1. "Are there any hard technical constraints? (specific cloud provider, language, framework, existing systems to integrate with)"
2. "Budget constraints? Free tier only, limited spend, or flexible?"
3. "Team constraints? Solo dev, small team, specific skill sets?"

### Non-Functional Requirements
4. "Performance — any latency/throughput targets?"
5. "Scalability — what's the expected load now vs. 12 months?"
6. "Availability — how bad is downtime? (hobby project vs. business critical)"
7. "Security — what data do we handle? Any compliance requirements?"

### Sizing
8. "How much data do we process/store? Rough estimates."
9. "How many users/requests per day?"

## GENERATION:

Generate `02-constraints-nfr.md` using template. Show for review.

"Here are the Constraints & NFRs:

[show content]

[A] Approve and continue
[E] Edit"

## NEXT STEP:

After approval, update frontmatter `stepsCompleted: [1, 2, 3]`, then load `./step-04-building-blocks.md`.
