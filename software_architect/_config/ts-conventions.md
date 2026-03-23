# TypeScript Conventions (Layer 3)

> Stable. These rules apply to every stage that produces or reviews TypeScript.

## Compiler Settings
```json
{
  "compilerOptions": {
    "strict": true,
    "noUncheckedIndexedAccess": true,
    "exactOptionalPropertyTypes": true,
    "noImplicitReturns": true,
    "noFallthroughCasesInSwitch": true
  }
}
```

## Interfaces vs. Types
- `interface` — for object shapes that may be extended (domain entities, service contracts)
- `type` — for unions, intersections, mapped types, and aliases
- **Never use `any`.** Use `unknown` and narrow with type guards.
- **Never use `!` (non-null assertion)** — handle optionality explicitly.

## Naming
| Construct | Convention | Example |
|-----------|-----------|---------|
| Interface | PascalCase, no `I` prefix | `User`, `OrderRepository` |
| Type alias | PascalCase | `UserId`, `ApiResponse<T>` |
| Enum | PascalCase, values SCREAMING_SNAKE_CASE | `UserRole.ADMIN` |
| Function | camelCase | `getUserById` |
| File | kebab-case | `user-repository.ts` |
| Folder | kebab-case | `order-management/` |
| Constant | SCREAMING_SNAKE_CASE | `MAX_RETRY_COUNT` |

## Exports
- One primary export per file (named, not default)
- Barrel files (`index.ts`) only at module boundaries — not inside modules
- Re-export only what is part of the module's public API

## Generics
- Single-letter only for trivial utilities (`T`, `K`, `V`)
- Domain generics: descriptive — `TEntity`, `TResponse`, `TInput`

## Null & Undefined
- Prefer `undefined` over `null` for optional values
- Use optional chaining `?.` and nullish coalescing `??`
- Never assume a value is defined without narrowing first

## Error Handling
- Never `throw` raw strings — always throw typed `Error` subclasses
- Services return a `Result<T, E>` type — no unhandled promise rejections
- API layer catches domain errors and maps them to typed HTTP responses

## Async
- Always `async/await` — never raw `.then()` chains
- All async functions annotated with explicit `Promise<T>` return type
- Handle all rejection paths explicitly

## Zod Schemas
- Define Zod schemas as the single source of truth for external data shapes
- Derive TypeScript types from schemas: `type User = z.infer<typeof UserSchema>`
- Validate at system boundaries only (API inputs, external API responses, env vars)
