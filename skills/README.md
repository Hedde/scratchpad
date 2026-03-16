# Skill System

> Skills are composable, self-improving procedures. They can be invoked by the orchestrator,
> by agents, or directly. Each skill defines a clear input, process, and output.

## Architecture

```
skills/
  ├── _template.md            # Base template for new skills
  ├── bootstrap-interview.md  # Project setup & tech stack discovery
  ├── implement.md            # Feature implementation workflow
  ├── code-review.md          # Structured code review
  ├── design-review.md        # Architecture evaluation
  ├── test-generate.md        # Test creation & strategy
  ├── coverage-check.md       # Coverage analysis
  ├── debug.md                # Systematic debugging
  ├── refactor.md             # Safe refactoring
  ├── doc-update.md           # MANDATORY post-task documentation (used by ALL agents)
  ├── doc-audit.md            # Documentation health check
  ├── adr-create.md           # Architecture Decision Record creation
  └── security-audit.md       # Security vulnerability check
```

## How Skills Work

1. An agent (or the orchestrator) identifies a skill needed for the task
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
