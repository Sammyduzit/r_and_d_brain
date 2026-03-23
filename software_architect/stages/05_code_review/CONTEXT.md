# Stage 05 — Code Review (Layer 2)

## Inputs
- Layer 4 (working):   `../04_system_design/output/system_design.md`
- Layer 4 (working):   `../04_system_design/output/interfaces.ts`
- Layer 4 (working):   `output/code_input/` ← implementation code to review (place files here)
- Layer 3 (reference): `../../_config/ts-conventions.md`
- Layer 3 (reference): `../../_config/code-standards.md`
- Layer 3 (reference): `../../_config/design-patterns.md`

## Process

**If `output/code_input/` contains code files:** review the implementation.
**If `output/code_input/` is empty:** produce a pre-implementation checklist from the system design.

### When reviewing code — check per file/module:
1. **Interface adherence** — does the implementation match `interfaces.ts` contracts exactly?
2. **Convention compliance** — `ts-conventions.md` and `code-standards.md` followed?
3. **Pattern compliance** — correct design patterns applied per `design-patterns.md`?
4. **Type safety** — any `any`, unsafe casts, missing type guards, or implicit `unknown`?
5. **Error handling** — all error paths covered per the strategy in `system_design.md`?
6. **Test coverage** — right things being tested per the testing strategy?

**Format per finding:**
```
[FILE: path/to/file.ts — LINE: N]
[✅ OK | ⚠️ SUGGESTION | ❌ VIOLATION]
Rule violated: ... (reference to ts-conventions.md / code-standards.md)
Suggested fix: ...
```

### When producing a pre-implementation checklist:
Produce a module-by-module checklist a developer can use during implementation to ensure compliance before code review.

## Outputs
- `code_review.md` → `output/`
