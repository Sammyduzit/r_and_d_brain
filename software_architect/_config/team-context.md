# Team Context (Layer 3)

## Pipeline Roles

| Role | Person | Workspace | Responsibility |
|------|--------|-----------|----------------|
| Product Manager | Anca Afloroaei | `pm_workspace/` | PRD creation, user advocacy, edge cases, dependency mapping |
| Software Architect | Samuel Marone | `software_architect/` | Architecture, technical specs, TypeScript interfaces, code review |
| Critic / QA | Markus Beermann | `critic_workspace/` | Test adapters, E2E suites, architecture compliance checks |

## Pipeline Flow

```
PM System
  └─ output: prd_input.md
        ↓
Software Architect  (this workspace)
  └─ output: system_design.md, interfaces.ts, code_review.md
        ↓
Critic System
  └─ output: test_suite.md, compliance_report.md
```

## Handoff Convention
- All handoffs are plain `.md` or `.ts` files placed in the receiving workspace's `01_context_creation/output/` folder
- Human review at every stage boundary — no automated stage transitions
- If a stage produces a ❌ Blocker, the pipeline stops until a human resolves it

## Workspace Principles
- **LLM-agnostic:** all files readable by any model
- **No framework lock-in:** orchestration lives in the filesystem
- **Anyone can contribute:** pipeline changes = editing `.md` files, no coding required
- **Git-compatible:** every workspace is a folder that can be versioned, diffed, and branched
