# Claude Code Orchestrator

A project scaffolding template that extends Claude Code beyond what `/init` provides. Where `/init` generates a static `CLAUDE.md` with project conventions, this template adds a **self-improving agent team**, **composable skills**, and **structured collaboration protocols** that evolve with your project.

## Why not just `/init`?

`/init` is a great starting point: it scans your codebase and produces a single `CLAUDE.md` with conventions, commands, and structure. But it stops there. It gives you a snapshot, not a system.

This template adds three layers on top:

| Layer | What it does | Why it matters |
|-------|-------------|----------------|
| **Agent team** | 10 named specialists (security, QA, UX, performance, database, planning, dev, debugging, testing, docs) that review, vote, and collaborate | Consistent multi-perspective review instead of ad-hoc prompting |
| **Skill system** | Reusable procedures for common workflows (implement, debug, refactor, test, review, etc.) | Repeatable quality instead of reinventing the process each time |
| **Self-improvement** | Agents record gotchas and lessons learned; repetitive patterns auto-promote to skills and conventions | The system gets smarter the more you use it |

## When to use this

- **Complex or long-running projects** where consistency and knowledge retention matter
- **Team-style development** where you want structured review from multiple perspectives (security, performance, UX)
- **Projects that evolve** where capturing lessons and conventions pays off over time

For small scripts or one-off tasks, `/init` is sufficient.

## Getting started

1. Clone this template into your project (or use it as a starting point)
2. Run the bootstrap interview — it auto-detects existing projects or interviews you for new ones:
   ```
   Follow skills/bootstrap-interview.md
   ```
3. The bootstrap fills in all `[NOT YET CONFIGURED]` sections in `CLAUDE.md` and configures agents for your stack

## Structure

```
CLAUDE.md                 # Orchestrator — routes tasks to agents, skills, and docs
agents/                   # Named specialist agents (see agents/README.md)
skills/                   # Composable procedures (see skills/README.md)
docs/                     # Living project documentation (see docs/README.md)
```

## The team

```
ROLE AGENTS (Advisors — review, audit, recommend)
  Lisa (UX) · Mark (QA) · Daan (Perf) · Sophie (DB) · Eva (Security)

TASK AGENTS (Executors — plan, build, fix, test, document)
  Thomas (Plan) · Rick (Dev) · Karin (Fix) · Sanne (Test) · Niels (Docs)
```

Role agents advise and review but never implement. Task agents execute. The user orchestrates. See [agents/README.md](agents/README.md) for spawn patterns and collaboration protocols.

## Key concepts

- **Voting protocol** — agents vote APPROVE / CONCERN / BLOCK at checkpoints. Sophie and Eva have automatic BLOCK rights on data integrity and critical security issues.
- **Team assembly patterns** — predefined workflows per task type (feature, bugfix, refactor, security-sensitive, etc.)
- **Mandatory documentation** — Niels (docs agent) runs after every task. Documentation updates are non-negotiable.
- **Periodic tuning** — run `/loop 4h /insights` during development to auto-detect repetitive patterns and promote them to conventions.

## License

MIT
