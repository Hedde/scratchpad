# AI Quality Bootstrap

A project scaffolding template for starting projects from a quality approach instead of ad-hoc prompting. It gives Claude Code and Codex the same shared blueprint: a **self-improving agent team**, **composable skills**, and **structured collaboration protocols** that evolve with your project.

## Why not just `/init`?

`/init` is a great starting point: it scans your codebase and produces a single tool-specific instruction file with conventions, commands, and structure. But it stops there. It gives you a snapshot, not a system.

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
CLAUDE.md                 # Canonical project blueprint and Claude Code entry point
AGENTS.md                 # Thin Codex adapter; points back to the same blueprint
.claude/                  # Claude-native rules, settings, and native skill wrappers
agents/                   # Cross-tool named specialist personas (see agents/README.md)
skills/                   # Cross-tool composable procedures (see skills/README.md)
agent-briefs/             # Reusable prompt templates
docs/                     # Living project documentation (see docs/README.md)
```

See [docs/development/ai-tooling.md](docs/development/ai-tooling.md) for the no-drift adapter rules, including when repo-root `.agents/` is valid for Codex plugin metadata.

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
- **Periodic tuning** — `/sprint-retro` immediately after each sprint, `/loop 24h /insights` for daily system-wide tuning, `/loop 336h /maintainability-audit` every 2 weeks. Insights needs accumulated lessons to be useful — running it more often than daily produces empty reports.

## License

MIT
