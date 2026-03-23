# Stage 01 — Context Creation (Layer 2)

## Inputs
- Layer 4 (working): `output/prd_input.md` ← PRD delivered by PM System

## Process
Analyze the PRD and produce a structured context document that all subsequent stages will reference.

The output must be concise and complete — every stage downstream depends on it being correct.

Produce `context.md` with exactly these sections:

1. **Project Summary** — what is being built, in two sentences maximum
2. **Functional Requirements** — numbered list of discrete features the system must deliver
3. **Non-Functional Requirements** — performance, security, scalability, and reliability constraints
4. **User Types** — who uses the system and what their primary goals are
5. **Key Constraints** — technical, business, or timeline constraints that restrict design choices
6. **Open Questions** — ambiguities in the PRD that must be resolved before architecture can be finalized

Rules:
- Do not add assumptions. If the PRD is unclear, list it as an Open Question.
- Do not propose solutions yet. This stage is understanding only.
- Keep requirements atomic — one requirement per line, testable in isolation.

## Outputs
- `context.md` → `output/`
