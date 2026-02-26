# Documentation

Living documentation that grows with the project. Claude uses these files as context when working on tasks.

## Structure

```
docs/
  architecture/           # System design, database patterns, infrastructure decisions
    database.md           # DB design, connection pooling, query patterns
  decisions/              # Architecture Decision Records (ADRs)
    _template.md          # ADR template
  development/            # How to build: workflow, code patterns, testing
    code-organization.md  # Module structure, naming, separation of concerns
    migrations.md         # Database migration conventions and safe patterns
    testing.md            # Test strategy, types, coverage targets
    workflow.md           # Dev environment, commands, CI, commit conventions
  features/               # Functional documentation per feature
    _template.md          # Feature doc template
  getting-started/        # Onboarding
    new-feature-checklist.md  # Step-by-step guide for adding features
  operations/             # Deployment, monitoring, CI/CD
    deployment.md         # Deployment process, infrastructure, troubleshooting
    ci.md                 # CI/CD pipeline configuration
  ui/                     # Frontend patterns
    patterns.md           # Component architecture, styling conventions
```

## How Documentation Evolves

This documentation system is designed to **learn and improve** over time:

1. **Templates** (`_template.md`) provide starting structure for new entries
2. **Docs are updated** as patterns are discovered, refined, or deprecated
3. **CLAUDE.md** always points to the right doc for the right task
4. **Feature docs** are created for every non-trivial feature before implementation
5. **Decision records** capture the "why" behind architectural choices

## Principles

- **Living docs**: Update when patterns change. Delete when obsolete
- **DRY**: Detail lives here. CLAUDE.md only holds summaries and pointers
- **Examples first**: Show code examples, not just rules
- **Honest**: Mark things as `[TODO]` rather than guessing. Fill in when known
