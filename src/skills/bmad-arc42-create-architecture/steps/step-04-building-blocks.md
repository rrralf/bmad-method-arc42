# Step 4: Building Block View

## MANDATORY EXECUTION RULES:

- 📖 Read complete step file before acting
- 🛑 Do NOT generate content without user input
- ✅ Collaborate — ask questions, propose, refine together
- ✅ Communicate in {communication_language}, write output in {document_output_language}

## OUTPUT:

`{architecture_output}/1-architecture/04-building-blocks.md`

## YOUR TASK:

Collaboratively define the system's building blocks at two levels of detail, their published contracts, and the core domain model. Arc42 §5.

## IMPORTANT DISTINCTIONS:

- **Building blocks** = static decomposition (floor plan). What the system is made of.
- **Runtime view** (step 05) = how blocks interact at runtime. How the system works.
- **Contracts** = each block defines what it *exposes* and what it *consumes*. Blocks are like Lego bricks — they define their shape, not who connects to them.
- **DDD bounded contexts** may align with Level 1 blocks, but don't force it. Building blocks are about decomposition, bounded contexts are about semantic boundaries.

## DISCOVERY SEQUENCE:

### Level 1: System Decomposition

1. "Decompose the system into 3-7 major blocks. Each block = one clear responsibility. Think C4 containers, not classes."
2. For each block, propose a pre-filled **Building Block Canvas** based on what you've read from input documents:

```
Block: {name}
┌─────────────────────────────────────────┐
│ Responsibility: {proposed}              │
│ Boundaries:     IN: ... OUT: ... NOT:   │
│ Technology:     {proposed}              │
│ NFR overrides:  {proposed}              │
│ Risks:          {proposed}              │
└─────────────────────────────────────────┘
```

Ask the user to confirm or correct each canvas.

3. "How do these blocks communicate? For each boundary — is it sync (REST/gRPC) or async (events/queues/streams)?"

### Contracts (per block)

4. For each block, propose:

**Exposes (published contracts):**
| Contract | Type (OpenAPI/AsyncAPI) | Schema | Description |

**Consumes (required inputs):**
| Contract | Type | From | Description |

Ask: "Does this block expose or consume anything else?"

### Level 2: Internal Structure (selective)

5. "Which blocks need deeper documentation? (complex, risky, novel — not all blocks need Level 2)"
6. For selected blocks: "What are the key internal components?"

### Domain Model

7. "What are the core domain entities? How do they transform as they flow between blocks?"

Propose entity table and flow diagram based on input documents.

## DIAGRAM:

Propose a C4 Level 2 (Container) diagram showing all Level 1 blocks and their connections. Can be PlantUML or Mermaid.

Save diagram to `{architecture_output}/diagrams/` if user approves.

## GENERATION:

Generate `04-building-blocks.md` using template `./templates/04-building-blocks.tmpl.md`.

Show the generated content to the user for review:

"Here's the Building Block View. Please review:

[show content]

[A] Approve and continue
[E] Edit — tell me what to change"

## NEXT STEP:

After approval, update README.md frontmatter, then load `./step-05-runtime.md`.
