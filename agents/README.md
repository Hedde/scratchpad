# Agent System

> Agents are reusable AI specialist personas that work in **teams**. Each agent has a defined role,
> assigned skills, and improves itself after every use. Agents collaborate, review each other's work,
> and report to the Orchestrator (team lead) who makes the final call.

## Architecture

```
CLAUDE.md (Trigger File / Orchestrator Entry Point)
  │
  ├── agents/
  │   ├── _template.md        # Base template for new agents
  │   ├── orchestrator.md     # TEAM LEAD: assembles teams, final reviewer, authorizes commits
  │   ├── architect.md        # System design, patterns, decisions
  │   ├── developer.md        # Implementation, coding, debugging
  │   ├── reviewer.md         # DEDICATED REVIEWER: quality, security (never implements)
  │   ├── tester.md           # Testing strategy, test writing
  │   └── documenter.md       # Documentation maintenance (mandatory after all tasks)
  │
  └── skills/                 # Composable procedures agents invoke
      └── (see skills/README.md)
```

## Prerequisites

For full team collaboration, Claude must be configured in **team/multi-agent mode**.
In single-agent mode, one agent assumes all roles sequentially.

## How Teams Work

### 1. Task Arrives
The Orchestrator (team lead) assesses the task and reads `CLAUDE.md`.

### 2. Team Assembly & Briefing
The Orchestrator selects agents and briefs them with:
- The task description and context
- Their teammates' **handles** (references to other agent files)
- The workflow and handoff sequence
- Expectations: collaborate, review, discuss

### 3. Collaborative Execution
Agents work in phases. After each phase:
- The producing agent presents its output
- Teammates review and provide feedback (peer review)
- Discussion happens if there are disagreements
- The team reaches consensus (or the Orchestrator decides)

### 4. Dedicated Review
The Reviewer agent reviews code quality, security, and convention adherence.
The Reviewer does NOT implement — they only review.
Other agents also peer-review at checkpoints, but the Reviewer is the dedicated quality gate.

### 5. Reports to Orchestrator
Each agent reports: what was done, decisions made, and any unresolved concerns.

### 6. Final Review by Orchestrator
The Orchestrator (team lead) reviews the aggregate output:
- Quality, conventions, documentation
- Resolved and unresolved disagreements
- Overall coherence with user request

### 7. Commit Authorization
**Only the Orchestrator authorizes commits.** No agent may commit independently.
This ensures all work is reviewed, documented, and approved before entering the codebase.

### 8. Self-Improvement (MANDATORY)
After task completion, every involved agent MUST:
- Update its own `## Lessons Learned` section
- Trigger `skills/doc-update.md` for documentation updates
- Report improvements back to the orchestrator

## Creating a New Agent

1. Copy `_template.md` to `<agent-name>.md`
2. Fill in all sections — leave nothing as placeholder
3. Assign skills from `skills/` (or create new ones)
4. Add the agent to the table in `CLAUDE.md`
5. Commit with `feat: add <agent-name> agent`

## Agent Design Principles

- **Team-first** — Agents collaborate, they don't work in isolation
- **Single responsibility** — Each agent does one thing well
- **Skill-based** — Agents use skills for procedures, not inline logic
- **Self-improving** — Every use makes the agent better
- **Context-aware** — Agents always read `CLAUDE.md` for project state
- **Composable** — Agents work together in teams
- **Reusable** — Design agents for repeated use across tasks
- **No solo commits** — Only the Orchestrator authorizes commits
