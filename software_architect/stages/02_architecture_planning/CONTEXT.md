# Stage 02 — Architecture Planning (Layer 2)

## Inputs
- Layer 4 (working):   `../01_context_creation/output/context.md`
- Layer 3 (reference): `../../_config/tech-stack.md`
- Layer 3 (reference): `../../_config/design-patterns.md`

## Process
Design the high-level architecture for the system described in `context.md`.

Produce `architecture_blueprint.md` with exactly these sections:

1. **Architecture Style** — which pattern and why (must be from `design-patterns.md`)
2. **Module Map** — list of top-level modules with single-line responsibility statements
3. **Data Flow** — how data moves through the system (text or ASCII diagram)
4. **Core TypeScript Interfaces** — the 3–7 domain interfaces that anchor the entire design
5. **Technology Decisions** — specific framework/library choices per layer, each justified against `tech-stack.md`
6. **Dependency Graph** — which modules depend on which (no circular dependencies allowed)

Rules:
- Every architectural decision must address a requirement from `context.md`. If it doesn't, remove it.
- Do not introduce patterns not listed in `design-patterns.md` without explicit written justification.
- If a requirement cannot be addressed with the approved tech stack, flag it — do not silently deviate.

## Outputs
- `architecture_blueprint.md` → `output/`
