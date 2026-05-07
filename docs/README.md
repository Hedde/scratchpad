# Documentation

Living documentation that grows with the project. Part of a self-improving system together with `agents/` and `skills/`.

## System Architecture

```
CLAUDE.md                     # Canonical project blueprint and Claude Code entry point
AGENTS.md                     # Thin Codex adapter; points back to CLAUDE.md
.claude/                      # Claude-native rules, settings, and skill wrappers
agents/                       # Named specialist personas (Role + Task agents)
  ├── ux-designer.md          # Lisa — UI patterns, accessibility, responsive design
  ├── qa-lead.md              # Mark — Production readiness, quality dimensions
  ├── performance-engineer.md # Daan — Runtime performance at scale
  ├── database-specialist.md  # Sophie — Schema, migrations, data integrity
  ├── security-engineer.md    # Eva — OWASP, access control, threat modeling
  ├── plan.md                 # Thomas — Implementation planning (zero code)
  ├── feature.md              # Rick — Full-stack implementation
  ├── fix.md                  # Karin — Root cause analysis, bug fixes
  ├── test.md                 # Sanne — Test strategy, coverage improvement
  └── docs-sync.md            # Niels — Documentation sync (automatic)
skills/                       # Composable procedures used by agents
  ├── bootstrap-interview.md, implement.md, code-review.md, ...
  └── doc-update.md           # [MANDATORY] post-task skill — triggered by Niels
docs/                         # Project knowledge base (this folder)
  ├── architecture/           # System design, database patterns
  ├── decisions/              # Architecture Decision Records (ADRs)
  ├── development/            # Workflow, code patterns, testing, migrations
  ├── features/               # Functional documentation per feature
  ├── getting-started/        # Onboarding, checklists
  ├── operations/             # Deployment, CI/CD
  └── ui/                     # Frontend patterns
```

Tool-specific details live in [development/ai-tooling.md](development/ai-tooling.md). Keep adapters thin so Claude, Codex, and future runtimes do not drift apart.

## How Documentation Evolves

Documentation updates are **[MANDATORY] after every task**. This is enforced by:

1. Niels (docs-sync agent) triggers `skills/doc-update.md` as the final step
2. `CLAUDE.md` explicitly requires documentation updates as non-negotiable
3. Agent `Gotchas` and `Lessons Learned` sections grow with every correction and task
4. Skill `Improvement Log` sections grow with every use

## Documentation Map

When working on a task, consult the relevant docs AND the relevant agents/skills.

| When working on... | Consult Docs | Agents | Skills |
|--------------------|-------------|--------|--------|
| New project setup | All docs | User (bootstrap) | `bootstrap-interview` |
| New feature | [Feature Checklist](getting-started/new-feature-checklist.md) | Thomas → Rick + Sanne + reviewers | `implement`, `test-generate` |
| Database changes | [Database](architecture/database.md), [Migrations](development/migrations.md) | Thomas → Sophie → Rick | `implement` |
| Architecture decisions | [Decision Records](decisions/) | Thomas + Sophie + Daan | `design-review`, `adr-create` |
| Writing tests | [Testing](development/testing.md) | Sanne | `test-generate`, `coverage-check` |
| Code review | [Code Organization](development/code-organization.md) | Mark + Eva + Lisa (fan-out) | `code-review`, `security-audit` |
| UI work | [UI Patterns](ui/patterns.md) | Lisa → Rick + Lisa review | `implement` |
| Bug fix | [Testing](development/testing.md) | Karin + Sanne + Mark | `debug`, `test-generate` |
| Refactoring | [Code Organization](development/code-organization.md) | Thomas → Rick + Mark | `refactor`, `code-review` |
| Performance | [Code Organization](development/code-organization.md) | Daan → Rick/Karin + Daan verify | `debug`, `implement` |
| **After ANY task** | **All affected docs** | **Niels [MANDATORY]** | **`doc-update`** |
| **End of sprint** | — | — | **`sprint-retro`** |

## Principles

- **Living docs**: Update when patterns change. Delete when obsolete
- **DRY**: Detail lives here. CLAUDE.md only holds summaries and pointers
- **Examples first**: Show code examples, not just rules
- **Honest**: Mark things as `[NOT YET CONFIGURED]` rather than guessing. Fill in when known
- **Mandatory**: Documentation is not optional. It happens after every task
