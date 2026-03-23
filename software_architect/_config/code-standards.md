# Code Standards (Layer 3)

> Stable. Applies to all code produced or reviewed in this pipeline.

## Module File Structure
```
module-name/
  index.ts                   ← public API (re-exports only — no logic)
  module-name.types.ts       ← interfaces and type aliases
  module-name.schema.ts      ← Zod schemas
  module-name.service.ts     ← application logic
  module-name.repository.ts  ← data access (infrastructure)
  module-name.test.ts        ← unit tests
```

## Functions
- Max **20 lines** per function — extract if longer
- Max **3 parameters** — use an options object (`opts: { ... }`) beyond that
- Pure functions preferred — side effects isolated to the infrastructure layer
- Functions do one thing. Name them accordingly.

## Comments
- No comments explaining **what** the code does — the code should be self-explanatory
- Comments explain **why** (business reason, non-obvious trade-off, regulatory constraint)
- JSDoc only on public module API surface (`index.ts` exports)

## Imports
- Absolute imports via TypeScript path aliases: `import { User } from '@/modules/user'`
- Relative imports allowed only within the same module folder
- `../../../` is a code smell — indicates a missing abstraction or misplaced file

## Testing Requirements
| Layer | What to test | How |
|-------|-------------|-----|
| Domain | Entity invariants, business rules | Unit (pure functions) |
| Application | Use case orchestration | Unit with mocked repos |
| Infrastructure | Repository queries, external calls | Integration (real DB / MSW) |
| API | Request/response contracts, auth | Integration |
| E2E | Critical user flows | Playwright |

Test behaviour, not implementation. Do not test private methods.

## Commits & Branching
- Conventional commits: `feat:`, `fix:`, `chore:`, `refactor:`, `test:`, `docs:`
- Branch naming: `feature/`, `fix/`, `chore/`
- One logical change per PR

## Forbidden
| Rule | No exceptions |
|------|--------------|
| `any` type | Use `unknown` + type guard |
| `// @ts-ignore` | Fix the underlying type issue |
| `console.log` in production | Use a structured logger |
| Mutating function arguments | Return new values |
| Magic numbers/strings | Use named constants |
| `npm` or `yarn` commands | Use `pnpm` |
