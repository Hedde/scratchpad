# Project Blueprint — Orchestrator Trigger File

> **This file is the AI assistant's command center.** It routes every task to the right agents, skills, and documentation.
> This file is self-improving: after every completed task, update this file and relevant docs.
> Keep it concise — deep knowledge lives in `docs/`, agents in `agents/`, skills in `skills/`.

---

## CRITICAL RULES

1. **Documentation updates are MANDATORY.** After every completed task — no exceptions — update all relevant docs, this file, and any agent/skill that was involved. This is not optional. This is not "when appropriate." This is ALWAYS.
2. **Never leave `[NOT YET CONFIGURED]` after learning the answer.** Fill it in immediately.
3. **Agents are reusable.** Before creating a new agent, check `agents/` for an existing one. If none fits, create one from `agents/_template.md`.
4. **Skills are composable.** Skills can be invoked by the orchestrator or by agents. Check `skills/` before writing inline logic.
5. **Self-improvement is continuous.** Every agent, skill, and doc improves itself after use. Record what worked, what failed, and what to do differently.

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

## Conventions

> Conventions are discovered and codified. When a pattern works twice, it becomes a convention.
> Document here (summary) and in `docs/` (detail). This is MANDATORY.

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

> Agents are reusable specialists that work in **teams**. They review each other's work, discuss
> trade-offs, and reach consensus. The Orchestrator is the team lead who makes the final call
> and is the ONLY one who authorizes commits. See [agents/README.md](agents/README.md).
>
> **Prerequisite:** Claude must be configured in team/multi-agent mode for full team collaboration.
> In single-agent mode, one agent assumes all roles sequentially.

### How Agents Work Together

1. **Orchestrator assesses the task** and selects the team
2. **Team is briefed** — every agent receives the task + their teammates' handles
3. **Agents work in phases** — each phase ends with a peer review checkpoint
4. **Agents discuss and debate** — they review each other's output, raise concerns, propose alternatives
5. **Dedicated Reviewer** reviews code quality, security, and convention adherence
6. **Agents report to Orchestrator** — presenting work, decisions, and any unresolved concerns
7. **Orchestrator (team lead) reviews** — the final authority on quality and correctness
8. **Only after Orchestrator approval** — the commit happens and documentation is updated
9. **If no agent fits** — create one from `agents/_template.md` (reusable for future tasks)

### Available Agents

| Agent | File | Role in Team | Skills |
|-------|------|-------------|--------|
| Orchestrator | [agents/orchestrator.md](agents/orchestrator.md) | **Team lead** — assembles, coordinates, final reviewer, authorizes commits | All skills |
| Architect | [agents/architect.md](agents/architect.md) | System design, patterns, ADRs, tech decisions | `design-review`, `adr-create` |
| Developer | [agents/developer.md](agents/developer.md) | Implementation, coding, debugging | `implement`, `debug`, `refactor` |
| Reviewer | [agents/reviewer.md](agents/reviewer.md) | Dedicated reviewer — quality, security, conventions | `code-review`, `security-audit` |
| Tester | [agents/tester.md](agents/tester.md) | Test strategy, test writing, coverage | `test-generate`, `coverage-check` |
| Documenter | [agents/documenter.md](agents/documenter.md) | Documentation guardian — always invoked | `doc-update`, `doc-audit` |

> **To add a new agent:** Copy `agents/_template.md`, fill it in, add a row to this table.

### Team Assembly Patterns

| Task Type | Team | Workflow |
|-----------|------|----------|
| New feature | Architect + Developer + Tester + Reviewer + Documenter | Design → Peer Review → Implement → Peer Review → Test → Review → Document → **Orchestrator Approval** → Commit |
| Bug fix | Developer + Tester + Documenter | Debug → Fix → Peer Review → Test → Document → **Orchestrator Approval** → Commit |
| Refactor | Architect + Developer + Reviewer + Documenter | Plan → Peer Review → Refactor → Review → Document → **Orchestrator Approval** → Commit |
| New project setup | Orchestrator (runs bootstrap) | Interview → Configure → Verify → **Orchestrator Approval** → Commit |
| Code review | Reviewer + Documenter | Review → Document → **Orchestrator Approval** |
| Architecture decision | Architect + Developer + Documenter | Analyze → Team Discussion → Decide → ADR → **Orchestrator Approval** → Commit |

### Collaboration Protocol

- **Peer review at every checkpoint** — agents review each other's output before the next phase
- **Discussion is encouraged** — agents debate approaches and raise concerns openly
- **Reviewer is dedicated** — the Reviewer agent does not implement; it only reviews
- **Conflicts go to the Orchestrator** — unresolved disagreements are decided by the team lead
- **No solo commits** — the Orchestrator authorizes all commits after final review
- **Reports to Orchestrator** — each agent reports: what was done, decisions made, concerns raised
- **Repetition detection** — if an agent does something manually for the 2nd time, it logs this in its Repetition Log and proposes a new skill to the Orchestrator

---

## Skill System

> Skills are composable procedures. They can be invoked by the orchestrator, by agents, or directly.
> Skills are self-improving: after each use, the skill file is updated with lessons learned.
> See [skills/README.md](skills/README.md) for the full skill catalog.

### Available Skills

| Skill | File | Used By | Purpose |
|-------|------|---------|---------|
| Bootstrap Interview | [skills/bootstrap-interview.md](skills/bootstrap-interview.md) | Orchestrator | Project setup, tech stack discovery |
| Code Review | [skills/code-review.md](skills/code-review.md) | Reviewer | Structured code review process |
| Design Review | [skills/design-review.md](skills/design-review.md) | Architect | Architecture & design evaluation |
| Implementation | [skills/implement.md](skills/implement.md) | Developer | Feature implementation workflow |
| Test Generation | [skills/test-generate.md](skills/test-generate.md) | Tester | Test creation & coverage strategy |
| Documentation Update | [skills/doc-update.md](skills/doc-update.md) | All agents | MANDATORY post-task documentation |
| Refactor | [skills/refactor.md](skills/refactor.md) | Developer | Safe refactoring with verification |
| Debug | [skills/debug.md](skills/debug.md) | Developer | Systematic debugging process |
| ADR Create | [skills/adr-create.md](skills/adr-create.md) | Architect | Architecture Decision Record creation |
| Security Audit | [skills/security-audit.md](skills/security-audit.md) | Reviewer | Security vulnerability assessment |
| Coverage Check | [skills/coverage-check.md](skills/coverage-check.md) | Tester | Test coverage analysis |
| Doc Audit | [skills/doc-audit.md](skills/doc-audit.md) | Documenter | Documentation completeness check |
| Insights | [skills/insights.md](skills/insights.md) | Orchestrator | Periodic system tuning via `/loop` |

> **To add a new skill:** Copy `skills/_template.md`, fill it in, add a row to this table.
>
> **Periodic tuning:** Run `/loop 30m /insights` during active development to auto-detect repetitive patterns, promote conventions, and tune agent performance.

---

## Documentation Map (Trigger Reference)

> When working on a task, consult the relevant docs AND the relevant agents/skills.

| When working on... | Consult Docs | Consult Agent | Use Skill |
|--------------------|-------------|---------------|-----------|
| New project setup | All docs | Orchestrator | `bootstrap-interview` |
| New feature | [Feature Checklist](docs/getting-started/new-feature-checklist.md) | Architect → Developer → Tester | `implement`, `test-generate` |
| Database changes | [Database](docs/architecture/database.md), [Migrations](docs/development/migrations.md) | Architect → Developer | `implement` |
| Architecture decisions | [Decision Records](docs/decisions/) | Architect | `design-review`, `adr-create` |
| Code structure | [Code Organization](docs/development/code-organization.md) | Developer | `implement` |
| Writing tests | [Testing Strategy](docs/development/testing.md) | Tester | `test-generate`, `coverage-check` |
| Code review | [Code Organization](docs/development/code-organization.md) | Reviewer | `code-review`, `security-audit` |
| UI work | [UI Patterns](docs/ui/patterns.md) | Developer | `implement` |
| Deployment | [Deployment](docs/operations/deployment.md) | Orchestrator | — |
| CI/CD | [CI/CD](docs/operations/ci.md) | Orchestrator | — |
| Bug fix | [Testing](docs/development/testing.md) | Developer → Tester | `debug`, `test-generate` |
| Refactoring | [Code Organization](docs/development/code-organization.md) | Architect → Developer → Reviewer | `refactor`, `code-review` |
| **After ANY task** | **All affected docs** | **Documenter** | **`doc-update` (MANDATORY)** |

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

## Self-Improvement Protocol

> **This section governs how the entire system evolves.** Every agent, skill, and doc follows this.

### MANDATORY Post-Task Updates (Non-Negotiable)

After EVERY completed task, the following MUST happen:

1. **Run `skills/doc-update.md`** — The Documenter agent (or the acting agent) updates all affected documentation.
2. **Update this file** — If any section of CLAUDE.md was affected, update it now.
3. **Update agent files** — Every agent involved records what it learned in its `## Lessons Learned` section.
4. **Update skill files** — Every skill used records improvements in its `## Improvement Log` section.
5. **Replace `[NOT YET CONFIGURED]`** — If any information was discovered, fill it in immediately.
6. **Create feature docs** — For any new feature: `docs/features/<feature-name>.md`.
7. **Create ADRs** — For any architectural decision: `docs/decisions/NNN-title.md`.

### Self-Improvement Triggers

| Event | Action | Who |
|-------|--------|-----|
| Task completed | Update all affected docs, agents, skills | All involved agents |
| **Repetitive task detected** | **Log in agent's Repetition Log; if 2nd occurrence → propose skill to Orchestrator** | **The detecting agent → Orchestrator** |
| Pattern works twice | Promote to convention in CLAUDE.md + docs | Documenter |
| Mistake found | Record in agent's lessons + update relevant docs | The agent that erred |
| New tech introduced | Create/update agent + skills for it | Orchestrator |
| User gives feedback | Update conventions, agent behavior, skill procedures | Orchestrator |
| `[NOT YET CONFIGURED]` encountered | Run bootstrap or ask user | Orchestrator |
| Agent created | Add to CLAUDE.md agent table | Orchestrator |
| Skill created | Add to CLAUDE.md skill table | Orchestrator |
| **`/insights` runs** | **Harvest lessons, detect repetition, promote conventions, tune agents** | **Orchestrator** |

### Periodic Tuning

Run `skills/insights.md` periodically to keep the system sharp:

```bash
# During active development (recommended)
/loop 30m /insights

# During maintenance
/loop 2h /insights

# After a sprint or release (thorough one-time run)
/insights
```

The insights skill scans all agent Repetition Logs, Lessons Learned, and Skill Improvement Logs to:
- Auto-create skills for detected repetitive patterns
- Promote confirmed patterns to conventions
- Tune agent configurations
- Flag documentation gaps

### Quality Gates

Before implementing any feature, verify:
1. Is there a feature doc in `docs/features/`? **If not, create one first.**
2. Do the architecture docs cover the patterns being used?
3. Are test patterns documented for this type of code?
4. Are the right agents and skills identified for this task?
5. Is the UI approach consistent with documented patterns?

After implementing any feature, verify:
1. **Were all docs updated?** (This is mandatory, check again.)
2. Were agent lessons recorded?
3. Were skill improvements logged?
4. Does CLAUDE.md reflect the current state?
