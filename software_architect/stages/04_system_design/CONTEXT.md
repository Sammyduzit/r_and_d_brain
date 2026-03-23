# Stage 04 — System Design (Layer 2)

## Inputs
- Layer 4 (working):   `../02_architecture_planning/output/architecture_blueprint.md`
- Layer 4 (working):   `../03_plan_review/output/plan_review.md`
- Layer 3 (reference): `../../_config/tech-stack.md`
- Layer 3 (reference): `../../_config/ts-conventions.md`
- Layer 3 (reference): `../../_config/code-standards.md`

## Process
Before starting: resolve all ❌ Blockers from `plan_review.md`. If a Blocker cannot be resolved without human input, stop and list what is needed.

Transform the reviewed blueprint into detailed, implementation-ready specifications.

Produce two files:

**`system_design.md`** — containing:
1. **Module Specifications** — for each module: responsibility, public API surface, internal structure, dependencies
2. **API Contracts** — all endpoints (path, method, request type, response type, error cases)
3. **Database Schema** — all entities, fields, types, and relationships
4. **Error Handling Strategy** — typed error classes, propagation rules, API translation
5. **Testing Strategy** — what to unit test vs. integration test per module, with examples

**`interfaces.ts`** — containing:
- All domain interfaces and types, production-ready and compilable
- Zod schemas for all API boundaries
- No placeholders, no `any`, no `TODO` comments

Rules:
- Follow `ts-conventions.md` strictly for all naming and typing.
- Follow `code-standards.md` for file structure and function design.
- Apply ⚠️ Suggestions from `plan_review.md` if they improve the design — note which ones you applied.

## Outputs
- `system_design.md` → `output/`
- `interfaces.ts` → `output/`
