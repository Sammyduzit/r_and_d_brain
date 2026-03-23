# Approved Architecture Patterns (Layer 3)

> Stable. Only patterns listed here may be used without explicit justification in the architecture blueprint.

## Primary: Hexagonal Architecture (Ports & Adapters)

Default for all full-stack applications.

```
         PRIMARY SIDE (Driving)
         ┌─────────────────────┐
         │  Next.js UI/Pages   │
         │  API Routes / tRPC  │  ← Primary Adapters
         │  Test Harnesses     │    (call the core via Primary Ports)
         └────────┬────────────┘
                  │ implements
         ┌────────▼────────────────────────────────────┐
         │            APPLICATION CORE                  │
         │  ┌──────────────────────────────────────┐   │
         │  │  Primary Ports (interfaces)           │   │
         │  │  e.g. ICreateUserUseCase              │   │
         │  ├──────────────────────────────────────┤   │
         │  │  Use Cases / Application Services     │   │
         │  ├──────────────────────────────────────┤   │
         │  │  Domain: Entities, Value Objects,     │   │
         │  │          Business Rules               │   │
         │  ├──────────────────────────────────────┤   │
         │  │  Secondary Ports (interfaces)         │   │
         │  │  e.g. IUserRepository, IEmailService  │   │
         │  └──────────────────────────────────────┘   │
         └────────────────────────┬────────────────────┘
                                  │ implements
         ┌────────────────────────▼────────────────┐
         │  PrismaUserRepository                    │
         │  SendGridEmailAdapter                    │  ← Secondary Adapters
         │  StripePaymentAdapter                    │    (called by the core via Secondary Ports)
         └─────────────────────────────────────────┘
         SECONDARY SIDE (Driven)
```

**Dependency rule:** the core defines the ports (interfaces). Adapters implement them. The core never imports from adapters.

### What lives where

| Location | Contains |
|----------|----------|
| **Domain** | Entities, Value Objects, domain errors, domain events, business rules |
| **Application** | Use cases, Primary Port interfaces, Secondary Port interfaces, DTOs |
| **Primary Adapters** | Next.js routes/pages, tRPC routers, CLI handlers, test harnesses |
| **Secondary Adapters** | Prisma repositories, external API clients, email/storage services |

### Ports in TypeScript
Ports are TypeScript interfaces. Adapters are their implementations.

```typescript
// Secondary Port — defined in Application layer
interface UserRepository {
  findById(id: UserId): Promise<User | undefined>
  save(user: User): Promise<void>
}

// Secondary Adapter — defined in Infrastructure layer
class PrismaUserRepository implements UserRepository {
  // ...Prisma implementation
}
```

This means: **`interfaces.ts` (Stage 04 output) is your Port document.**
Markus's Critic system tests against these interfaces — not the implementations.

---

## Repository Pattern
- All data access sits behind a Secondary Port interface defined in the Application layer
- Secondary Adapters provide the concrete implementation
- Enables swapping DB implementations without touching the core (real DB ↔ in-memory ↔ mock)

## Factory Pattern
- Complex entity construction (with validation or invariants) isolated in a factory function or class
- Factories live in the Domain layer — they enforce domain rules at creation time
- Prefer static factory methods over constructors for entities with business invariants

## Service Pattern (Use Cases)
- One use case class per discrete user action (e.g., `CreateUserUseCase`, `PlaceOrderUseCase`)
- Use cases orchestrate domain entities and secondary ports — no raw DB queries, no HTTP logic
- Implement the corresponding Primary Port interface

## Schema-First with Zod
- Zod schemas are the single source of truth for data entering the system at adapter boundaries
- TypeScript types derived from schemas: `type CreateUserInput = z.infer<typeof CreateUserSchema>`
- Validation happens at the adapter boundary only — inside the core, data is already trusted and typed

## Dependency Injection
- Use cases receive their Secondary Port dependencies via constructor injection
- Primary Adapters instantiate use cases and inject the correct adapters
- DI container (tsyringe, inversify) only if the graph becomes unmanageable — manual injection is preferred for clarity

---

## Patterns to Avoid

| Anti-pattern | Why |
|---|---|
| Business logic in Primary Adapters (routes, pages) | Belongs in use cases |
| Direct DB access outside Secondary Adapters | Violates the port contract |
| Core importing from adapters | Inverts the dependency rule |
| Circular dependencies between modules | Indicates a missing abstraction |
| God use case (> 5 public methods) | Split by user action |
| Shared mutable global state | Use dependency injection |
