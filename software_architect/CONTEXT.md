# Software Architect — Workspace Routing (Layer 1)

## Stage Overview

| Stage | Folder | Input | Output |
|-------|--------|-------|--------|
| 01 | `01_context_creation/` | `prd_input.md` (from PM) | `context.md` |
| 02 | `02_architecture_planning/` | `context.md` | `architecture_blueprint.md` |
| 03 | `03_plan_review/` | `architecture_blueprint.md` + `context.md` | `plan_review.md` |
| 04 | `04_system_design/` | `architecture_blueprint.md` + `plan_review.md` | `system_design.md`, `interfaces.ts` |
| 05 | `05_code_review/` | `system_design.md` + `interfaces.ts` + code | `code_review.md` |

## Global Resources (Layer 3)
- `_config/tech-stack.md` — approved technologies per layer
- `_config/ts-conventions.md` — TypeScript naming, typing, and export rules
- `_config/design-patterns.md` — approved architecture patterns
- `_config/code-standards.md` — file structure, function rules, testing requirements
- `_config/team-context.md` — team roles, handoff conventions, pipeline flow

## How to Run a Pipeline
1. Place the PRD in `stages/01_context_creation/output/prd_input.md`
2. Open `stages/01_context_creation/CONTEXT.md`
3. Execute the stage — review output — proceed to next stage

## Human Review Gates
Each stage **stops** after writing output. A human must review and optionally edit `output/` before the next stage reads it. This is intentional.
