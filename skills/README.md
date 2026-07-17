# Skill System

> Skills are composable, self-improving procedures. They can be invoked by the orchestrator,
> by agents, or directly. Each skill defines a clear input, process, and output.

## Catalog

| Skill | File | Purpose |
|-------|------|---------|
| Bootstrap | [bootstrap-interview.md](bootstrap-interview.md) | Project setup, tech stack discovery |
| Implementation | [implement.md](implement.md) | Feature implementation workflow |
| Code Review | [code-review.md](code-review.md) | Structured code review |
| Design Review | [design-review.md](design-review.md) | Architecture evaluation |
| Test Generation | [test-generate.md](test-generate.md) | Test creation & strategy |
| Coverage Check | [coverage-check.md](coverage-check.md) | Coverage analysis |
| Debug | [debug.md](debug.md) | Systematic debugging |
| Refactor | [refactor.md](refactor.md) | Safe refactoring |
| Doc Update | [doc-update.md](doc-update.md) | **[MANDATORY]** post-task documentation |
| Doc Audit | [doc-audit.md](doc-audit.md) | Documentation completeness check |
| ADR Create | [adr-create.md](adr-create.md) | Architecture Decision Record |
| Security Audit | [security-audit.md](security-audit.md) | Security vulnerability check |
| Sprint Retro | [sprint-retro.md](sprint-retro.md) | Immediate post-sprint learning capture |
| Maintainability Audit | [maintainability-audit.md](maintainability-audit.md) | Periodic SIG/ISO 25010 macro-audit (Mark) |
| Insights | [insights.md](insights.md) | Periodic system tuning via `/loop` |
| Token Audit | [token-audit.md](token-audit.md) | Audit context overhead (CLAUDE.md, hooks, MCPs, skills) |
| Trigger Tree | [github.com/Hedde/trigger_tree](https://github.com/Hedde/trigger_tree) | `/tt status\|watch\|insights\|help` — doc-telemetrie, untouched/dead paden, router aanscherpen |

## Cadence

- `/sprint-retro` — immediately after each completed sprint (fresh signal)
- `/loop 24h /insights` — daily during active development; `/loop 168h /insights` during maintenance
- `/loop 336h /maintainability-audit` — every 2 weeks (macro code-quality audit by Mark)
- `/token-audit` — monthly, or whenever sessions feel slow / quotas tighten
- `/tt insights` — wekelijks tijdens actieve ontwikkeling; vereist ~30 read-events / 3 sessies aan telemetrie

> Insights is only useful with accumulated data (several completed tasks). Don't run more than once a day — empty reports waste context.

## How Skills Work

1. An agent (or the user) identifies a skill needed for the task
2. The skill file is read for the procedure
3. The procedure is followed step-by-step
4. After execution, the skill's `## Improvement Log` is updated with lessons learned

## Creating a New Skill

1. Copy `_template.md` to `<skill-name>.md`
2. Fill in all sections
3. Assign the skill to relevant agents in their agent files
4. Add the skill to the table in `CLAUDE.md`
5. Commit with `feat: add <skill-name> skill`

## Skill Design Principles

- **Procedural** — A skill is a series of steps, not a vague description
- **Self-improving** — Every use adds to the improvement log
- **Composable** — Skills can invoke other skills
- **Idempotent** — Running a skill twice should be safe
- **Context-aware** — Skills read `CLAUDE.md` for project state
