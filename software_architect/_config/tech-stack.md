# Tech Stack — TypeScript Full-Stack (Layer 3)

> Stable. Update only when the team makes a deliberate stack decision. Any deviation must be documented in the architecture blueprint with justification.

## Language & Runtime
- **TypeScript 5.x** — strict mode, `noUncheckedIndexedAccess: true`
- **Node.js 20+ LTS**

## Frontend
- Framework: **Next.js 14+** (App Router)
- Styling: **Tailwind CSS**
- Client state: **Zustand**
- Server state / data fetching: **TanStack Query**
- Forms: **React Hook Form** + **Zod**

## Backend
- Runtime: Node.js via **Next.js API routes** (default) or standalone **Fastify** (if separate backend needed)
- API style: **REST** (default) | **tRPC** (if full type-safety across client/server boundary is required)
- Validation: **Zod** — schemas shared between frontend and backend
- Auth: **Auth.js (NextAuth v5)**

## Database
- ORM: **Prisma**
- Default DB: **PostgreSQL**
- Migrations: **Prisma Migrate**

## Testing
- Unit & integration: **Vitest**
- E2E: **Playwright**
- Component: **Testing Library**
- API mocking: **MSW**

## Tooling
- Package manager: **pnpm**
- Monorepo (if multi-package): **Turborepo**
- Linting: **ESLint** (flat config) + **Prettier**
- Pre-commit: **Husky** + **lint-staged**
- CI: **GitHub Actions**

## Deployment
- Default: **Vercel**
- Self-hosted: **Docker** + **docker-compose**
