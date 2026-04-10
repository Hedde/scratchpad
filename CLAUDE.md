# Project Blueprint — Orchestrator Trigger File

> **This file is the AI assistant's command center.** It routes every task to the right agents, skills, and documentation.
> This file is self-improving: after every completed task, update this file and relevant docs.
> Keep it concise — deep knowledge lives in `docs/`, agents in `agents/`, skills in `skills/`.

---

## CRITICAL RULES

> Rules use RFC 2119 keywords: **[MUST]** = mandatory, **[SHOULD]** = recommended unless justified,
> **[COULD]** = optional, **[MUST NOT]** = prohibited.

1. **[MUST] Documentation updates after every task.** No exceptions — update all relevant docs, this file, and any agent/skill that was involved. This is not optional. This is not "when appropriate." This is ALWAYS.
2. **[MUST] Never leave `[NOT YET CONFIGURED]` after learning the answer.** Fill it in immediately.
3. **[MUST] Agents auto-improve on correction.** When an agent is corrected on a mistake or gotcha, it **[MUST]** update its own agent file: add to `## Gotchas` and `## Lessons Learned`. This is non-negotiable.
4. **[SHOULD] Reuse agents.** Before creating a new agent, check `agents/` for an existing one. If none fits, create one from `agents/_template.md`.
5. **[SHOULD] Skills over inline logic.** Skills are composable procedures. Check `skills/` before writing inline logic.
6. **[MUST] Self-improvement is continuous.** Every agent, skill, and doc improves itself after use. Record what worked, what failed, and what to do differently.
7. **[SHOULD] Not overly defensive.** Validate at system boundaries (user input, external APIs), but trust internal code and framework guarantees. No error handling for scenarios that can't happen, no fallbacks for hypothetical cases. Follow real code paths.
8. **[MUST] Copy existing patterns first.** Before building anything, find a similar feature/page in the codebase and copy its approach. When in doubt, ask the user.

---

## Approach Selection

> These rules prevent the #1 cause of wasted time: choosing the wrong approach.

- **Copy existing patterns first** — ALWAYS find a similar feature/page in the codebase and copy its approach. Ask the user if unsure
- **Server-side first** — NEVER use client-side workarounds (JS hacks, inline event handlers) when a server-side solution is possible
- **No hardcoding** — if something should be configurable or dynamic, design it that way from the start. Don't hardcode first and refactor later
- **Minimal fix** — for bugs: fix the specific problem, not the surrounding code. A placeholder text fix doesn't need an architectural analysis
- **UI: propose BEFORE implementing** — for EVERY UI/styling change: describe in 1-2 sentences what you'll do and wait for confirmation. First attempts often miss the mark
- **Unknown UX pattern? ASK — don't guess** — if there's no documented pattern or similar screen, present concrete options to the user. Record the decision so the question isn't asked again

## Output-First Workflow

> Sessions fail when the agent reads too long without producing anything. Produce output quickly, iterate.

- **Read, then produce** — after initial orientation: state your approach in 3 bullets, then continue reading if needed
- **Bug fix**: diagnosis + fix proposal BEFORE scanning the entire codebase
- **Planning**: start writing as soon as you know enough, mark unknowns as `[OPEN]` instead of reading more files
- **When in doubt: ask the user** instead of reading more files
- **Never >10 file reads without writing something** — if you've read 10 files and haven't produced output, you're over-researching

---

## Bootstrap: Auto-Discovery Protocol

> The bootstrap process is itself a skill: `skills/bootstrap-interview.md`
> It handles BOTH existing and new projects automatically.

**If any section is marked `[NOT YET CONFIGURED]`, the bootstrap MUST run before work begins.**

### How Bootstrap Works

The bootstrap skill **first detects** whether this is an existing or new project:

**Existing project detected** (source files, package manifests, configs found):
1. **Discover first, ask later** — scan the entire codebase for tech stack, patterns, conventions, commands
2. **Present a discovery report** — show findings to the user: "I found X, Y, Z — is this correct?"
3. **User confirms or corrects** — only ask questions about things that couldn't be discovered
4. Update all docs, agents, and skills with confirmed information

**New project detected** (no source code found):
1. **Decisions first** — nothing to discover, so interview the user about all choices
2. Ask about purpose, tech stack, environment, conventions, deployment
3. Update all docs, agents, and skills with decided information

In both cases:
- Immediately update this file, all docs, all agents, all skills
- Configure project-specific agent behavior and skill procedures
- Create stack-specific agents/skills if needed
- Never leave a section unconfigured after learning the answer

---

## Project Identity

- **Name:** [NOT YET CONFIGURED]
- **Description:** [NOT YET CONFIGURED]
- **Repository:** [NOT YET CONFIGURED]

## Tech Stack

[NOT YET CONFIGURED] — Run `skills/bootstrap-interview.md`

## Project Structure

[NOT YET CONFIGURED] — Auto-populated after bootstrap.

```
# Updated automatically as the project takes shape.
```

## Development

[NOT YET CONFIGURED] — See [docs/development/workflow.md](docs/development/workflow.md)

## Path-Specific Rules

`.claude/rules/` contains convention files with glob frontmatter. They load automatically when editing matching files — more efficient than putting everything in CLAUDE.md. Use `_template.md` to create new rules.

| Rule file | Globs | What it enforces |
|-----------|-------|-----------------|
| [NOT YET CONFIGURED] | [after bootstrap] | [after bootstrap] |

> **After bootstrap:** create rules for each layer of your stack (e.g., models, views, migrations, tests).
> Each rule file should only contain conventions relevant to that file type.

## Quality Hooks

`.claude/settings.json` contains automated quality gates:

- **PostToolUse** (Edit/Write) — auto-formats after every file edit. [NOT YET CONFIGURED] after bootstrap.
- **Stop** — runs format check + compile/lint + static analysis when the session ends. [NOT YET CONFIGURED] after bootstrap.

> **After bootstrap:** configure these hooks with your project's formatter, compiler, and linter commands.

## Conventions

> Conventions are discovered and codified. When a pattern works twice, it becomes a convention.
> Document here (summary) and in `docs/` (detail). This is **[MANDATORY]**.

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

## Agent System — Named Team

> Named specialist agents that work in **teams**. Role agents advise and review. Task agents
> plan, build, fix, test, and document. The user orchestrates.
> See [agents/README.md](agents/README.md) for full protocol and spawn examples.

### The Team

```
┌─────────────────────────────────────────────────────────────┐
│  ROLE AGENTS (Advisors — review, audit, recommend)          │
│  Lisa (UX) · Mark (QA) · Daan (Perf) · Sophie (DB) · Eva   │
├─────────────────────────────────────────────────────────────┤
│  TASK AGENTS (Executors — plan, build, fix, test, document) │
│  Thomas (Plan) · Rick (Dev) · Karin (Fix) · Sanne (Test)   │
│  Niels (Docs)                                               │
└─────────────────────────────────────────────────────────────┘
```

### Available Agents

| Name | File | Type | Focus |
|------|------|------|-------|
| **Lisa** | [agents/ux-designer.md](agents/ux-designer.md) | Role | UI consistency, accessibility, responsive design |
| **Mark** | [agents/qa-lead.md](agents/qa-lead.md) | Role | Production readiness, 5 quality dimensions |
| **Daan** | [agents/performance-engineer.md](agents/performance-engineer.md) | Role | Runtime performance at scale |
| **Sophie** | [agents/database-specialist.md](agents/database-specialist.md) | Role | Schema, migrations, data integrity |
| **Eva** | [agents/security-engineer.md](agents/security-engineer.md) | Role | OWASP Top 10, access control, threat modeling |
| **Thomas** | [agents/plan.md](agents/plan.md) | Task | Implementation planning (zero code) |
| **Rick** | [agents/feature.md](agents/feature.md) | Task | Full-stack implementation |
| **Karin** | [agents/fix.md](agents/fix.md) | Task | Root cause analysis, bug fixes |
| **Sanne** | [agents/test.md](agents/test.md) | Task | Test strategy, coverage improvement |
| **Niels** | [agents/docs-sync.md](agents/docs-sync.md) | Task | Documentation sync (automatic) |

> **To add a new agent:** Copy `agents/_template.md`, give it a name and persona, add a row here.

### Team Assembly Patterns

| Task Type | Team | Workflow |
|-----------|------|----------|
| New feature | Thomas → Rick + Sanne + fan-out review (Mark, Lisa, Eva) + Niels | Plan → Build → Test → Review → Docs |
| Bug fix | Karin + Sanne + Mark + Niels | Diagnose → Fix → Regression test → Preflight → Docs |
| Refactor | Thomas → Rick + Mark + Niels | Plan → Refactor → Quality review → Docs |
| Database change | Thomas → Sophie review → Rick + Daan review + Niels | Plan → Schema review → Build → Perf review → Docs |
| Security-sensitive | Thomas → Eva threat model → Rick + Eva review + Mark + Niels | Plan → Threat model → Build → Security review → Docs |
| UI feature | Thomas → Lisa design → Rick + Lisa review + Mark + Niels | Plan → UX design → Build → UX review → Docs |
| Performance issue | Daan audit → Karin/Rick + Daan verify | Audit → Fix → Verify improvement |
| Code review (PR) | Fan-out: Eva + Mark + Lisa → gather | Parallel review → Consensus → Summary |

### Collaboration Protocol

#### [MUST] Rules
- **Voting at every checkpoint** — agents vote APPROVE / CONCERN / BLOCK on each other's output
- **Role agents [MUST NOT] implement** — they advise, review, and recommend only
- **Every correction triggers auto-improve** — agent [MUST] update its own file with the lesson
- **Niels runs after every task** — documentation sync is automatic and mandatory
- **Repetition detection** — 2nd manual occurrence → agent [MUST] propose a skill

#### [SHOULD] Guidelines
- **Discussion before consensus** — agents [SHOULD] debate approaches and raise concerns
- **Fan-out for reviews** — multiple role agents [SHOULD] review in parallel, not sequentially
- **Present approach before building** — Rick [SHOULD] describe his plan in 3 bullets before multi-file changes

### Voting Protocol

When agents need to reach consensus (design decisions, readiness checks, risk assessments):

| Vote | Meaning | Blocks? |
|------|---------|---------|
| **APPROVE** | No issues from my perspective | No |
| **CONCERN** | Minor issues, can proceed with notes | No |
| **BLOCK** | Critical issues, [MUST] be resolved first | **Yes** |

**Consensus = zero BLOCKs + majority APPROVE.**
- Sophie and Eva have **automatic BLOCK** on data integrity and CRITICAL security issues respectively.
- Blockers [MUST] specify exactly what needs to change.
- If consensus cannot be reached, the user makes the final call.

### Estimation Protocol

When the team estimates effort:
1. Each agent estimates independently from their perspective (prevents anchoring)
2. Estimates [MUST] be shared simultaneously
3. If estimates differ >2x → discussion round to understand why
4. Final estimate = team median + risk buffer from highest outlier
5. Confidence level [MUST] always be stated: HIGH / MEDIUM / LOW

### Agent Communication

```python
# Spawn with name
Agent(subagent_type: "plan", name: "thomas", prompt: "design feature X")

# Send message to running agent
SendMessage(to: "thomas", message: "Sophie recommends adding an index on user_id")

# Fan-out review
Agent(subagent_type: "security-engineer", name: "eva", prompt: "review diff")
Agent(subagent_type: "qa-lead", name: "mark", prompt: "review diff")
Agent(subagent_type: "ux-designer", name: "lisa", prompt: "review diff")

# Parallel build in worktrees
Agent(subagent_type: "feature", name: "rick-backend", isolation: "worktree", prompt: "build API")
Agent(subagent_type: "feature", name: "rick-frontend", isolation: "worktree", prompt: "build UI")
```

### Development Lifecycle

Every significant change follows these phases. Not every task needs all phases — a small bug fix can start at Build.

```
  PLAN          BUILD         VERIFY        REVIEW        SHIP
┌─────────┐   ┌─────────┐   ┌─────────┐   ┌─────────┐   ┌─────────┐
│ Thomas  │──▸│  Rick   │──▸│ Sanne  │──▸│ Mark    │──▸│  User   │
│  Plan   │   │  Code   │   │  Test  │   │ Lisa    │   │ Commit  │
│         │   │  Impl   │   │  Debug │   │ Eva     │   │  Push   │
└─────────┘   └─────────┘   └─────────┘   └─────────┘   └─────────┘
```

| Phase | Who | Quality Gate |
|-------|-----|-------------|
| **Plan** | Thomas (plan) | User approves plan |
| **Build** | Rick (feature) / Karin (fix) | Compiles without warnings (automated via PostToolUse hook) |
| **Verify** | Sanne (test) | Tests green, coverage adequate |
| **Review** | Mark + Lisa + Eva (parallel) | No BLOCKs, majority APPROVE |
| **Ship** | User | Format + lint + compile clean (automated via Stop hook) |

**Quality gates at Build and Ship are automated via hooks** — see `.claude/settings.json`. This means agents get immediate feedback on formatting and compile errors without manual intervention.

### Parallel Agent Isolation

When multiple agents work in parallel on non-overlapping files **without** worktree isolation:

- **NEVER touch others' files** — no resets, fixes, or formatting on files you didn't change. This also applies to the orchestrator: if an agent breaks something, report to the user and **wait for instructions**. NEVER run `git checkout` or edits on another agent's files.
- **Report and wait** — if you hit a compile/lint error in someone else's file: report which file, which error, which agent likely caused it, and WAIT.
- **Format only your own files** — run the formatter only on files you changed, not project-wide (project-wide formatting breaks on syntax errors from other agents).
- **Compile errors from others block you?** — report to the user. Do NOT try to fix it yourself.

This prevents agents from overwriting each other's work or making conflicting fixes.

### Auto-Improvement Protocol

> **[MUST]** — This is the mechanism that makes agents smarter over time.

When an agent is corrected on a mistake, gotcha, or suboptimal approach:

1. **[MUST] Update `## Gotchas`** in its own agent file — add the specific pitfall with context
2. **[MUST] Update `## Lessons Learned`** — record what happened and the correct approach
3. **[SHOULD] Check for pattern** — is this a gotcha that affects other agents too?
4. **[SHOULD] Propose skill** — if this is the 2nd occurrence, propose a reusable skill

Format for gotcha entries:
```markdown
## Gotchas
- **[SHORT TITLE]** — [what goes wrong] → [correct approach]. Discovered: [date]
```

This ensures agents never make the same mistake twice.

---

## Skill System

> Skills are composable procedures. They can be invoked by the orchestrator, by agents, or directly.
> Skills are self-improving: after each use, the skill file is updated with lessons learned.
> See [skills/README.md](skills/README.md) for the full skill catalog.

### Available Skills

| Skill | File | Used By | Purpose |
|-------|------|---------|---------|
| Bootstrap Interview | [skills/bootstrap-interview.md](skills/bootstrap-interview.md) | User | Project setup, tech stack discovery |
| Code Review | [skills/code-review.md](skills/code-review.md) | Mark (QA) | Structured code review process |
| Design Review | [skills/design-review.md](skills/design-review.md) | Thomas (Plan) | Architecture & design evaluation |
| Implementation | [skills/implement.md](skills/implement.md) | Rick (Dev) | Feature implementation workflow |
| Test Generation | [skills/test-generate.md](skills/test-generate.md) | Sanne (Test) | Test creation & coverage strategy |
| Documentation Update | [skills/doc-update.md](skills/doc-update.md) | Niels (Docs) | **[MANDATORY]** post-task documentation |
| Refactor | [skills/refactor.md](skills/refactor.md) | Rick (Dev) | Safe refactoring with verification |
| Debug | [skills/debug.md](skills/debug.md) | Karin (Fix) | Systematic debugging process |
| ADR Create | [skills/adr-create.md](skills/adr-create.md) | Thomas (Plan) | Architecture Decision Record creation |
| Security Audit | [skills/security-audit.md](skills/security-audit.md) | Eva (Security) | Security vulnerability assessment |
| Coverage Check | [skills/coverage-check.md](skills/coverage-check.md) | Sanne (Test) | Test coverage analysis |
| Doc Audit | [skills/doc-audit.md](skills/doc-audit.md) | Niels (Docs) | Documentation completeness check |
| Insights | [skills/insights.md](skills/insights.md) | User | Periodic system tuning via `/loop` |

> **To add a new skill:** Copy `skills/_template.md`, fill it in, add a row to this table.
>
> **Periodic tuning:** Run `/loop 4h /insights` during active development to auto-detect repetitive patterns, promote conventions, and tune agent performance.

---

## Documentation Map (Trigger Reference)

> When working on a task, consult the relevant docs AND the relevant agents/skills.

| When working on... | Consult Docs | Agents | Skills |
|--------------------|-------------|--------|--------|
| New project setup | All docs | User (runs bootstrap) | `bootstrap-interview` |
| New feature | [Feature Checklist](docs/getting-started/new-feature-checklist.md) | Thomas → Rick + Sanne + reviewers | `implement`, `test-generate` |
| Database changes | [Database](docs/architecture/database.md), [Migrations](docs/development/migrations.md) | Thomas → Sophie → Rick | `implement` |
| Architecture decisions | [Decision Records](docs/decisions/) | Thomas + Sophie + Daan | `design-review`, `adr-create` |
| Code structure | [Code Organization](docs/development/code-organization.md) | Rick | `implement` |
| Writing tests | [Testing Strategy](docs/development/testing.md) | Sanne | `test-generate`, `coverage-check` |
| Code review | [Code Organization](docs/development/code-organization.md) | Mark + Eva + Lisa (fan-out) | `code-review`, `security-audit` |
| UI work | [UI Patterns](docs/ui/patterns.md) | Lisa → Rick + Lisa review | `implement` |
| Deployment | [Deployment](docs/operations/deployment.md) | — | — |
| CI/CD | [CI/CD](docs/operations/ci.md) | — | — |
| Bug fix | [Testing](docs/development/testing.md) | Karin + Sanne + Mark | `debug`, `test-generate` |
| Refactoring | [Code Organization](docs/development/code-organization.md) | Thomas → Rick + Mark | `refactor`, `code-review` |
| Performance issue | [Code Organization](docs/development/code-organization.md) | Daan → Rick/Karin + Daan verify | `debug`, `implement` |
| **After ANY task** | **All affected docs** | **Niels [MANDATORY]** | **`doc-update`** |

---

## Architecture Patterns

> Document proven patterns here as they emerge. Link to `docs/architecture/` for deep dives.

[NOT YET CONFIGURED] — Patterns will be documented as the project evolves.

See:
- [docs/architecture/database.md](docs/architecture/database.md)
- [docs/architecture/](docs/architecture/)

## Deployment

[NOT YET CONFIGURED] — See [docs/operations/deployment.md](docs/operations/deployment.md)

## CI/CD

[NOT YET CONFIGURED] — See [docs/operations/ci.md](docs/operations/ci.md)

## Key Domain Concepts

[NOT YET CONFIGURED] — Document domain-specific terminology and business rules as they emerge.

---

## Quality Framework

> Inspired by ICTU Kwaliteitsaanpak and ISO 25010. Defines what "done" means and how quality is measured.

### Quality Dimensions

Every change is evaluated across these dimensions. Not every dimension applies to every change — use judgment.

| Dimension | What to check | Who checks |
|-----------|--------------|------------|
| **Correctness** | Does it do what it should? Edge cases handled? | Mark (QA) |
| **Security** | OWASP Top 10, access control, injection, data leaks? | Eva (Security) |
| **Performance** | N+1 queries, unnecessary computation, payload sizes? | Daan (Performance) |
| **Usability** | Consistent with UI patterns, intuitive, responsive? | Lisa (UX) |
| **Accessibility** | WCAG basics, keyboard navigation, screen reader? | Lisa (UX) |
| **Maintainability** | Complexity, module size, naming, code organization? | Mark (QA) |
| **Data integrity** | Constraints, migrations safe, rollback possible? | Sophie (DB) |

### Definition of Done

A task is **done** when ALL applicable items are true:

- [ ] Code compiles without warnings
- [ ] Formatter and linter pass (automated via hooks)
- [ ] Tests exist and pass for new/changed behavior
- [ ] Both happy path and error paths are tested
- [ ] Permission checks verified in frontend AND backend
- [ ] No security vulnerabilities introduced (OWASP Top 10)
- [ ] Documentation updated (feature docs, help context, inline where non-obvious)
- [ ] UI changes match existing patterns (or new pattern documented)
- [ ] No hardcoded values that should be configurable
- [ ] Technical debt identified and logged (not necessarily resolved)

> **Adapt this list:** After bootstrap, add project-specific items (e.g., migration rollback tested, accessibility checked).

### Traceability

> Every requirement should be traceable through implementation to tests.

- **Requirements → Implementation**: feature docs in `docs/features/` describe what should exist; code implements it
- **Implementation → Tests**: every module has corresponding test coverage; tests verify documented behavior
- **Tests → Requirements**: test descriptions reference the behavior they verify, not implementation details

When adding a feature: write the feature doc first, implement second, test third. This creates natural traceability.

### Technical Debt Management

Technical debt is normal and acceptable — but it must be **visible** and **planned**.

- **Make it visible** — when you encounter or introduce tech debt, log it (TODO with context, or issue)
- **Don't hide it** — a known shortcut is better than a hidden one. Comment WHY the shortcut was taken
- **Plan payoff** — reserve ~10% of effort for debt reduction. Don't let it accumulate silently
- **Distinguish debt types**: intentional shortcuts (acceptable) vs. accidental mess (fix now)

---

## Self-Improvement Protocol

> **This section governs how the entire system evolves.** Every agent, skill, and doc follows this.

### [MANDATORY] Post-Task Updates

After EVERY completed task, the following **[MUST]** happen:

1. **Niels runs `skills/doc-update.md`** — updates all affected documentation
2. **Update CLAUDE.md** — if any section was affected, update it now
3. **Agent auto-improve** — every agent involved **[MUST]** record what it learned:
   - `## Gotchas` — new pitfalls discovered (with date and context)
   - `## Lessons Learned` — what worked, what didn't, what to do differently
4. **Skill improvement** — every skill used **[SHOULD]** update its `## Improvement Log`
5. **Replace `[NOT YET CONFIGURED]`** — if information was discovered, fill it in immediately
6. **Create feature docs** — for any new feature: `docs/features/<feature-name>.md`
7. **Create ADRs** — for any architectural decision: `docs/decisions/NNN-title.md`

### Self-Improvement Triggers

| Event | Action | Who | Priority |
|-------|--------|-----|----------|
| Agent corrected on mistake | **[MUST]** Update `## Gotchas` + `## Lessons Learned` in agent file | The corrected agent | **[MUST]** |
| Task completed | Update all affected docs, agents, skills | All involved agents | **[MUST]** |
| Repetitive task (2nd occurrence) | Log in Repetition Log → propose skill | Detecting agent → User | **[MUST]** |
| Pattern works twice | Promote to convention in CLAUDE.md + docs | Niels | **[SHOULD]** |
| New tech introduced | Create/update agent + skills for it | User | **[SHOULD]** |
| User gives feedback | Update conventions, agent behavior, skill procedures | User | **[MUST]** |
| `[NOT YET CONFIGURED]` encountered | Run bootstrap or ask user | User | **[MUST]** |
| Agent created | Add to CLAUDE.md agent table | User | **[MUST]** |
| Skill created | Add to CLAUDE.md skill table | User | **[MUST]** |
| `/insights` runs | Harvest lessons, detect repetition, promote conventions, tune agents | User | **[SHOULD]** |

### Periodic Tuning

Run `skills/insights.md` periodically to keep the system sharp:

```bash
# During active development (~2-3x per workday)
/loop 4h /insights

# During maintenance (once a day)
/loop 8h /insights

# After a sprint or release (thorough one-time run)
/insights
```

> Insights needs accumulated data — don't run it too often. A few completed tasks
> need to have happened for patterns to emerge.

The insights skill scans all agent Repetition Logs, Lessons Learned, and Skill Improvement Logs to:
- Auto-create skills for detected repetitive patterns
- Promote confirmed patterns to conventions
- Tune agent configurations
- Flag documentation gaps

### Quality Gates

**Before** implementing any feature — **[MUST]** verify:
1. Is there a feature doc in `docs/features/`? If not, create one first.
2. Do the architecture docs cover the patterns being used?
3. Are test patterns documented for this type of code?
4. Are the right agents identified for this task?
5. Is the UI approach consistent with documented patterns?

**After** implementing any feature — **[MUST]** verify:
1. Definition of Done checklist passes (see Quality Framework above)
2. Were all docs updated? (This is **[MANDATORY]**, check again.)
3. Were agent gotchas and lessons updated?
4. Were skill improvements logged?
5. Does CLAUDE.md reflect the current state?
6. Did all agents vote? Is consensus reached?
7. Was technical debt introduced? If yes, is it logged and visible?
