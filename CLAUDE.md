# Project Blueprint — Orchestrator Trigger File

> **This file is the AI assistant's command center.** It routes every task to the right agents, skills, and documentation.
> The file is self-improving: after every completed task, update this file and relevant docs.
> Keep it concise — deep knowledge lives in `docs/`, agents in `agents/`, skills in `skills/`.

---

## CRITICAL RULES

> Rules use RFC 2119 keywords: **[MUST]** = mandatory, **[SHOULD]** = recommended unless justified,
> **[COULD]** = optional, **[MUST NOT]** = prohibited.

1. **[MUST] Documentation updates after every task.** Update all relevant docs, this file, and any agent/skill that was involved. Not optional.
2. **[MUST] Never leave `[NOT YET CONFIGURED]` after learning the answer.** Fill it in immediately.
3. **[MUST] Agents auto-improve on correction.** When corrected on a mistake or gotcha, the agent **[MUST]** update its own file: `## Gotchas` and `## Lessons Learned`.
4. **[SHOULD] Reuse agents.** Before creating a new agent, check `agents/`. If none fits, create one from `agents/_template.md`.
5. **[SHOULD] Skills over inline logic.** Check `skills/` before writing inline procedures.
6. **[MUST] Self-improvement is continuous.** Every agent, skill, and doc improves itself after use.
7. **[SHOULD] Not overly defensive.** Validate at system boundaries (user input, external APIs), trust internal code and framework guarantees. No error handling for impossible scenarios.
8. **[MUST] Copy existing patterns first.** Find a similar feature/page and copy its approach. When in doubt, ask the user.

---

## Approach Selection

> These rules prevent the #1 cause of wasted time: choosing the wrong approach.

- **Copy existing patterns first** — ALWAYS find similar code and copy its approach.
- **Server-side first** — NEVER use client-side workarounds when a server-side solution is possible.
- **No hardcoding** — configurable/dynamic things must be designed that way from the start.
- **Minimal fix** — for bugs: fix the specific problem, not the surrounding code.
- **UI: propose BEFORE implementing** — describe in 1-2 sentences, wait for confirmation.
- **Unknown UX pattern? ASK — don't guess** — present concrete options, record the decision.

## Output-First Workflow

> Produce output quickly, iterate. Sessions fail when you read too long without producing.

- **Read, then produce** — after initial orientation: state your approach in 3 bullets.
- **Bug fix**: diagnosis + fix proposal BEFORE scanning the entire codebase.
- **Planning**: start writing as soon as you know enough, mark unknowns as `[OPEN]`.
- **When in doubt: ask the user** instead of reading more files.
- **Never >10 file reads without writing something.**

---

## Bootstrap

If any section below is marked `[NOT YET CONFIGURED]`, run `skills/bootstrap-interview.md` before work begins. Bootstrap auto-detects existing vs. new projects and fills in the gaps.

---

## Project Identity

- **Name:** [NOT YET CONFIGURED]
- **Description:** [NOT YET CONFIGURED]
- **Repository:** [NOT YET CONFIGURED]

## Tech Stack

[NOT YET CONFIGURED] — Run `skills/bootstrap-interview.md`

## Project Structure

[NOT YET CONFIGURED] — Auto-populated after bootstrap.

## Development

[NOT YET CONFIGURED] — See [docs/development/workflow.md](docs/development/workflow.md)

## Path-Specific Rules

`.claude/rules/` contains convention files with glob frontmatter. They load automatically when editing matching files — more efficient than inlining everything in CLAUDE.md. Use `_template.md` to create new rules.

| Rule file | Globs | What it enforces |
|-----------|-------|------------------|
| [NOT YET CONFIGURED] | `e.g. lib/**/*.ex` | `e.g. Elixir code style, Credo rules` |
| [NOT YET CONFIGURED] | `e.g. test/**/*.exs` | `e.g. Test structure, factory patterns` |
| [NOT YET CONFIGURED] | `e.g. migrations/*` | `e.g. Migration safety, rollback rules` |

> **After bootstrap:** create one rule file per layer (models, views, migrations, tests).

## Quality Hooks

`.claude/settings.json` contains automated quality gates:

- **PostToolUse** (Edit/Write) — auto-formats after every edit. [NOT YET CONFIGURED] after bootstrap.
- **Stop** — runs format check + compile/lint + static analysis at session end. **Alternative**: use a git pre-commit hook instead of a Stop hook — that keeps quality checks out of Claude's context and only runs them when it matters (at commit time).

> **After bootstrap:** configure hooks with your project's formatter, compiler, and linter commands.

## Conventions

> Conventions are discovered and codified. When a pattern works twice, it becomes a convention.

### Code Style
[NOT YET CONFIGURED] — See [docs/development/code-organization.md](docs/development/code-organization.md)

### Database
[NOT YET CONFIGURED] — See [docs/architecture/database.md](docs/architecture/database.md)

### Naming
[NOT YET CONFIGURED]

### Testing
[NOT YET CONFIGURED] — See [docs/development/testing.md](docs/development/testing.md)

### Git
- Conventional commits: `feat:`, `fix:`, `chore:`, `refactor:`, `test:`, `docs:`
- See [docs/development/workflow.md](docs/development/workflow.md)

### UI & Design System
[NOT YET CONFIGURED] — See [docs/ui/patterns.md](docs/ui/patterns.md)

---

## Agent System

Named specialist agents work in **teams**. Role agents advise and review. Task agents plan, build, fix, test, document. The user orchestrates.

### The Team

| Name | File | Type | Focus |
|------|------|------|-------|
| **Lisa** | [agents/ux-designer.md](agents/ux-designer.md) | Role | UI consistency, accessibility, responsive design |
| **Mark** | [agents/qa-lead.md](agents/qa-lead.md) | Role | Production readiness, quality dimensions |
| **Daan** | [agents/performance-engineer.md](agents/performance-engineer.md) | Role | Runtime performance at scale |
| **Sophie** | [agents/database-specialist.md](agents/database-specialist.md) | Role | Schema, migrations, data integrity |
| **Eva** | [agents/security-engineer.md](agents/security-engineer.md) | Role | OWASP Top 10, access control, threat modeling |
| **Thomas** | [agents/plan.md](agents/plan.md) | Task | Implementation planning (zero code) |
| **Rick** | [agents/feature.md](agents/feature.md) | Task | Full-stack implementation |
| **Karin** | [agents/fix.md](agents/fix.md) | Task | Root cause analysis, bug fixes |
| **Sanne** | [agents/test.md](agents/test.md) | Task | Test strategy, coverage improvement |
| **Niels** | [agents/docs-sync.md](agents/docs-sync.md) | Task | Documentation sync (automatic) |

> **To add a new agent:** copy `agents/_template.md`, give it a name and persona, add a row here.

### Collaboration

For team protocols (workflow patterns, voting, consensus, multi-instance rules, SendMessage, parallel isolation): see **[agents/README.md](agents/README.md)**.

For reusable prompt templates (docs-audit, pr-review, feature-build, refactor-plan): see **[agent-briefs/](agent-briefs/README.md)** — saves 2-3k tokens per sprint versus writing briefs from scratch.

### Development Lifecycle

```
  PLAN          BUILD         VERIFY        REVIEW        SHIP
┌─────────┐   ┌─────────┐   ┌─────────┐   ┌─────────┐   ┌─────────┐
│ Thomas  │──▸│  Rick   │──▸│ Sanne   │──▸│ Mark    │──▸│  User   │
│  Plan   │   │  Code   │   │  Test   │   │ Lisa    │   │ Commit  │
│         │   │  Impl   │   │  Debug  │   │ Eva     │   │  Push   │
└─────────┘   └─────────┘   └─────────┘   └─────────┘   └─────────┘
```

| Phase | Who | Quality Gate |
|-------|-----|-------------|
| **Plan** | Thomas | User approves plan |
| **Build** | Rick / Karin | Compiles without warnings (automated) |
| **Verify** | Sanne | Tests green, coverage adequate |
| **Review** | Mark + Lisa + Eva (parallel) | No BLOCKs, majority APPROVE |
| **Ship** | User | See [docs/development/dod.md](docs/development/dod.md) |

Not every task needs all phases — small bug fixes can start at Build.

---

## Skill System

> Skills are composable procedures. Invoked by the orchestrator, by agents, or directly.
> See [skills/README.md](skills/README.md) for the full catalog.

| Skill | File | Purpose |
|-------|------|---------|
| Bootstrap | [skills/bootstrap-interview.md](skills/bootstrap-interview.md) | Project setup, tech stack discovery |
| Implementation | [skills/implement.md](skills/implement.md) | Feature implementation workflow |
| Code Review | [skills/code-review.md](skills/code-review.md) | Structured code review |
| Design Review | [skills/design-review.md](skills/design-review.md) | Architecture evaluation |
| Test Generation | [skills/test-generate.md](skills/test-generate.md) | Test creation & strategy |
| Coverage Check | [skills/coverage-check.md](skills/coverage-check.md) | Coverage analysis |
| Debug | [skills/debug.md](skills/debug.md) | Systematic debugging |
| Refactor | [skills/refactor.md](skills/refactor.md) | Safe refactoring |
| Doc Update | [skills/doc-update.md](skills/doc-update.md) | **[MANDATORY]** post-task documentation |
| Doc Audit | [skills/doc-audit.md](skills/doc-audit.md) | Documentation completeness check |
| ADR Create | [skills/adr-create.md](skills/adr-create.md) | Architecture Decision Record |
| Security Audit | [skills/security-audit.md](skills/security-audit.md) | Security vulnerability check |
| Sprint Retro | [skills/sprint-retro.md](skills/sprint-retro.md) | Immediate post-sprint learning capture |
| Insights | [skills/insights.md](skills/insights.md) | Periodic system tuning via `/loop` |

> **To add a new skill:** copy `skills/_template.md`, fill it in, add a row here.
>
> **Periodic tuning:** run `/loop 4h /insights` during active development. Run `/sprint-retro` immediately after each completed sprint.

---

## Documentation Map

> When working on a task, consult the relevant docs AND the relevant agents/skills.

| When working on... | Consult Docs | Agents | Skills |
|--------------------|-------------|--------|--------|
| New project setup | All docs | User (bootstrap) | `bootstrap-interview` |
| New feature | [Feature Checklist](docs/getting-started/new-feature-checklist.md) | Thomas → Rick + Sanne + reviewers | `implement`, `test-generate` |
| Database changes | [Database](docs/architecture/database.md), [Migrations](docs/development/migrations.md) | Thomas → Sophie → Rick | `implement` |
| Architecture decisions | [Decision Records](docs/decisions/) | Thomas + Sophie + Daan | `design-review`, `adr-create` |
| Writing tests | [Testing](docs/development/testing.md) | Sanne | `test-generate`, `coverage-check` |
| Code review | [Code Organization](docs/development/code-organization.md) | Mark + Eva + Lisa (fan-out) | `code-review`, `security-audit` |
| UI work | [UI Patterns](docs/ui/patterns.md) | Lisa → Rick + Lisa review | `implement` |
| Bug fix | [Testing](docs/development/testing.md) | Karin + Sanne + Mark | `debug`, `test-generate` |
| Refactoring | [Code Organization](docs/development/code-organization.md) | Thomas → Rick + Mark | `refactor`, `code-review` |
| Performance | [Code Organization](docs/development/code-organization.md) | Daan → Rick/Karin + Daan verify | `debug`, `implement` |
| **After ANY task** | **All affected docs** | **Niels [MANDATORY]** | **`doc-update`** |
| **End of sprint** | — | — | **`sprint-retro`** |

---

## Architecture Patterns

[NOT YET CONFIGURED] — Patterns will be documented as the project evolves.

See [docs/architecture/](docs/architecture/).

## Deployment

[NOT YET CONFIGURED] — See [docs/operations/deployment.md](docs/operations/deployment.md)

## CI/CD

[NOT YET CONFIGURED] — See [docs/operations/ci.md](docs/operations/ci.md)

## Key Domain Concepts

[NOT YET CONFIGURED] — Document domain-specific terminology and business rules as they emerge.

---

## Quality Framework

> Inspired by ICTU Kwaliteitsaanpak and ISO 25010.

### Quality Dimensions

Every change is evaluated across these dimensions. Not every dimension applies to every change — use judgment.

| Dimension | Who checks |
|-----------|------------|
| **Correctness** — does it do what it should? | Mark (QA) |
| **Security** — OWASP, access, data leaks | Eva (Security) |
| **Performance** — N+1, computation, payloads | Daan (Performance) |
| **Usability** — consistent, intuitive, responsive | Lisa (UX) |
| **Accessibility** — WCAG, keyboard, screen reader | Lisa (UX) |
| **Maintainability** — complexity, naming, organization | Mark (QA) |
| **Data integrity** — constraints, migrations safe | Sophie (DB) |

### Definition of Done

See **[docs/development/dod.md](docs/development/dod.md)** — full checklist with MUST/SHOULD/MAY criteria and skip-policy. Agents reference this instead of carrying their own checklists.

### Traceability

Every requirement should be traceable through implementation to tests. Feature doc first → implementation → test. Test descriptions reference documented behavior, not implementation details.

### Technical Debt

Debt is acceptable but must be **visible**:
- Log when encountered (TODO + context, or issue)
- Comment WHY shortcuts were taken
- Reserve ~10% of effort for debt reduction
- Distinguish intentional (acceptable) from accidental (fix now)

---

## Self-Improvement Protocol

### [MANDATORY] Post-Task Updates

After EVERY completed task:

1. **Niels runs `skills/doc-update.md`** — updates all affected documentation.
2. **Update CLAUDE.md** — if any section was affected.
3. **Agent auto-improve** — every involved agent records `## Gotchas` (new pitfalls) and `## Lessons Learned` (what worked/didn't).
4. **Skill improvement** — every used skill updates its `## Improvement Log`.
5. **Replace `[NOT YET CONFIGURED]`** — fill in immediately when information is discovered.
6. **Feature docs** — new features get `docs/features/<name>.md`.
7. **ADRs** — architectural decisions get `docs/decisions/NNN-title.md`.

### Self-Improvement Triggers

| Event | Action | Priority |
|-------|--------|----------|
| Agent corrected on mistake | Update `## Gotchas` + `## Lessons Learned` | [MUST] |
| Task completed | Update docs, agents, skills | [MUST] |
| Repetitive task (2nd occurrence) | Log in Repetition Log → propose skill | [MUST] |
| Pattern works twice | Promote to convention in CLAUDE.md + docs | [SHOULD] |
| New tech introduced | Create/update agent + skills | [SHOULD] |
| User gives feedback | Update conventions, agent behavior | [MUST] |
| `[NOT YET CONFIGURED]` encountered | Run bootstrap or ask user | [MUST] |
| Sprint completed | Run `skills/sprint-retro.md` | [SHOULD] |
| `/insights` runs | Harvest lessons, promote conventions, tune | [SHOULD] |

### Periodic Tuning

- **After each sprint** → `/sprint-retro` — immediate, focused learning capture
- **During active development** → `/loop 4h /insights` — periodic system-wide tuning
- **During maintenance** → `/loop 8h /insights`
- **After release** → `/insights` — thorough one-time run
