# Stage 03 — Plan Review (Layer 2)

## Inputs
- Layer 4 (working):   `../02_architecture_planning/output/architecture_blueprint.md`
- Layer 4 (working):   `../01_context_creation/output/context.md`
- Layer 3 (reference): `../../_config/design-patterns.md`
- Layer 3 (reference): `../../_config/ts-conventions.md`

## Process
Review the architecture blueprint against the original requirements and approved conventions.

Produce `plan_review.md` structured as follows — one entry per finding:

**Format per finding:**
```
[✅ APPROVED | ⚠️ SUGGESTION | ❌ BLOCKER] — [Section of blueprint]
Reason: ...
Action required: ... (only for ⚠️ and ❌)
```

Check for:
1. **Requirements coverage** — does every functional requirement in `context.md` map to an architectural component?
2. **Pattern compliance** — does the design follow `design-patterns.md`? Flag any unlisted pattern.
3. **TypeScript soundness** — are the proposed interfaces well-typed and consistent?
4. **Circular dependencies** — are there any between modules?
5. **Overengineering** — is any part of the design more complex than the requirements justify?
6. **Missing decisions** — any architectural choices left unresolved?

Rules:
- ❌ Blockers must be resolved by the human before Stage 04 begins.
- ⚠️ Suggestions are optional improvements — human decides whether to apply them.
- Do not rewrite the blueprint. Only review it.

## Outputs
- `plan_review.md` → `output/`

## Verify
Every functional requirement listed in `context.md` must appear in this review — either ✅ covered or ❌ missing.
