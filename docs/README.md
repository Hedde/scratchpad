# Documentation

Living documentation that grows with the project. Part of a self-improving system together with `agents/` and `skills/`.

## System Architecture

```
CLAUDE.md                     # Orchestrator trigger file — entry point for all tasks
  │
  ├── agents/                 # Named specialist personas (Role + Task agents)
  │   ├── ux-designer.md      # Lisa — UI patterns, accessibility, responsive design
  │   ├── qa-lead.md          # Mark — Production readiness, quality dimensions
  │   ├── performance-engineer.md  # Daan — Runtime performance at scale
  │   ├── database-specialist.md   # Sophie — Schema, migrations, data integrity
  │   ├── security-engineer.md     # Eva — OWASP, access control, threat modeling
  │   ├── plan.md             # Thomas — Implementation planning (zero code)
  │   ├── feature.md          # Rick — Full-stack implementation
  │   ├── fix.md              # Karin — Root cause analysis, bug fixes
  │   ├── test.md             # Sanne — Test strategy, coverage improvement
  │   └── docs-sync.md        # Niels — Documentation sync (automatic)
  │
  ├── skills/                 # Composable procedures used by agents
  │   ├── bootstrap-interview.md, implement.md, code-review.md, ...
  │   └── doc-update.md       # [MANDATORY] post-task skill — triggered by Niels
  │
  └── docs/                   # Project knowledge base (this folder)
      ├── architecture/       # System design, database patterns
      ├── decisions/          # Architecture Decision Records (ADRs)
      ├── development/        # Workflow, code patterns, testing, migrations
      ├── features/           # Functional documentation per feature
      ├── getting-started/    # Onboarding, checklists
      ├── operations/         # Deployment, CI/CD
      └── ui/                 # Frontend patterns
```

## How Documentation Evolves

Documentation updates are **[MANDATORY] after every task**. This is enforced by:

1. Niels (docs-sync agent) triggers `skills/doc-update.md` as the final step
2. `CLAUDE.md` explicitly requires documentation updates as non-negotiable
3. Agent `Gotchas` and `Lessons Learned` sections grow with every correction and task
4. Skill `Improvement Log` sections grow with every use

## Principles

- **Living docs**: Update when patterns change. Delete when obsolete
- **DRY**: Detail lives here. CLAUDE.md only holds summaries and pointers
- **Examples first**: Show code examples, not just rules
- **Honest**: Mark things as `[NOT YET CONFIGURED]` rather than guessing. Fill in when known
- **Mandatory**: Documentation is not optional. It happens after every task
