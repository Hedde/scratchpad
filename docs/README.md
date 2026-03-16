# Documentation

Living documentation that grows with the project. Part of a self-improving system together with `agents/` and `skills/`.

## System Architecture

```
CLAUDE.md                     # Orchestrator trigger file — entry point for all tasks
  │
  ├── agents/                 # Reusable AI specialist personas
  │   ├── orchestrator.md     # Team lead: assembles teams, coordinates, reviews final output
  │   ├── architect.md        # System design, patterns, ADRs
  │   ├── developer.md        # Implementation, debugging, refactoring
  │   ├── reviewer.md         # Code review, security, quality
  │   ├── tester.md           # Testing strategy, test writing, coverage
  │   └── documenter.md       # Documentation maintenance (mandatory after all tasks)
  │
  ├── skills/                 # Composable procedures used by agents
  │   ├── bootstrap-interview.md, implement.md, code-review.md, ...
  │   └── doc-update.md       # MANDATORY post-task skill — used by ALL agents
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

Documentation updates are **MANDATORY after every task**. This is enforced by:

1. Every agent triggers `skills/doc-update.md` as its final step
2. The Documenter agent exists solely to ensure documentation stays current
3. `CLAUDE.md` explicitly requires documentation updates as non-negotiable
4. Agent `Lessons Learned` sections grow with every task
5. Skill `Improvement Log` sections grow with every use

## Principles

- **Living docs**: Update when patterns change. Delete when obsolete
- **DRY**: Detail lives here. CLAUDE.md only holds summaries and pointers
- **Examples first**: Show code examples, not just rules
- **Honest**: Mark things as `[NOT YET CONFIGURED]` rather than guessing. Fill in when known
- **Mandatory**: Documentation is not optional. It happens after every task
