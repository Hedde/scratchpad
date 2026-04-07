# Agent System — Named Team

> Agents are named specialists that work in **teams**. Role agents advise and review.
> Task agents plan, build, fix, test, and document. The user orchestrates.

## The Team

```
┌─────────────────────────────────────────────────────────────┐
│  ROLE AGENTS (Advisors — review, audit, recommend)          │
│                                                             │
│  Lisa (UX)    Mark (QA)     Daan (Perf)                     │
│  Sophie (DB)  Eva (Security)                                │
├─────────────────────────────────────────────────────────────┤
│  TASK AGENTS (Executors — plan, build, fix, test, document) │
│                                                             │
│  Thomas (Plan)  Rick (Dev)    Karin (Fix)                   │
│  Sanne (Test)   Niels (Docs)                                │
└─────────────────────────────────────────────────────────────┘
```

## Agent Files

```
agents/
├── _template.md              # Base template for new agents
├── ux-designer.md            # Lisa — UI patterns, accessibility, responsive design
├── qa-lead.md                # Mark — Production readiness, quality dimensions
├── performance-engineer.md   # Daan — Runtime performance at scale
├── database-specialist.md    # Sophie — Schema, migrations, data integrity
├── security-engineer.md      # Eva — OWASP, access control, threat modeling
├── plan.md                   # Thomas — Implementation planning (zero code)
├── feature.md                # Rick — Full-stack implementation
├── fix.md                    # Karin — Root cause analysis, bug fixes
├── test.md                   # Sanne — Test strategy, coverage improvement
└── docs-sync.md              # Niels — Documentation sync (automatic)
```

## How to Spawn Agents

```python
# Single agent
Agent(subagent_type: "plan", name: "thomas", prompt: "plan feature X")

# Fan-out review (parallel)
Agent(subagent_type: "security-engineer", name: "eva", prompt: "review this diff")
Agent(subagent_type: "qa-lead", name: "mark", prompt: "review this diff")
Agent(subagent_type: "ux-designer", name: "lisa", prompt: "review this diff")

# Send feedback to a running agent
SendMessage(to: "thomas", message: "Sophie says add an index on user_id")

# Parallel build in worktrees
Agent(subagent_type: "feature", name: "rick-backend", isolation: "worktree", prompt: "build API")
Agent(subagent_type: "feature", name: "rick-frontend", isolation: "worktree", prompt: "build UI")
```

## Workflow Patterns

### Pattern 1: Solo
Single agent, simple task.
```
spawn feature("implement X")
```

### Pattern 2: Pipeline
Sequential — output feeds into the next step.
```
spawn plan → await → spawn feature → spawn qa-lead("review")
```

### Pattern 3: Fan-out Review
One change, multiple reviewers in parallel.
```
spawn security-engineer("review diff")  ─┐
spawn qa-lead("review diff")             ├─ gather → summary
spawn ux-designer("review diff")         ─┘
```

### Pattern 4: Parallel Build
Multiple developers, each on their own branch (worktree isolation).
```
spawn feature(name: "rick-1", isolation: "worktree", "build backend")
spawn feature(name: "rick-2", isolation: "worktree", "build frontend")
→ merge worktrees → spawn qa-lead("review whole")
```

### Pattern 5: Refinement
Plan → expert review → feedback → final plan.
```
1. spawn plan(name: "thomas", "design feature X")
2. parallel: database-specialist + performance-engineer review plan
3. SendMessage feedback to thomas
4. finalize → spawn feature
```

### Pattern 6: Full Team Sprint
Large feature, complete team in phases.
```
Phase 1 (Plan):    plan → refinement with database-specialist + performance-engineer
Phase 2 (Build):   feature × 2 parallel (worktrees)
Phase 3 (Review):  security-engineer + qa-lead + ux-designer parallel
Phase 4 (Polish):  fix (issues) → test (coverage)
Phase 5 (Ship):    docs-sync + qa-lead (preflight)
```

## Team Consensus Protocol

### Voting
When agents need to reach consensus (design decisions, readiness checks, risk assessment):

| Vote | Meaning |
|------|---------|
| **APPROVE** | No issues from my perspective |
| **CONCERN** | Minor issues, can proceed with notes |
| **BLOCK** | Critical issues, **[MUST]** be resolved first |

**Consensus = zero BLOCKs + majority APPROVE.**

- Sophie has **automatic BLOCK** on changes that compromise data integrity.
- Eva has **automatic BLOCK** on CRITICAL security vulnerabilities.
- Blockers **[MUST]** specify exactly what needs to change.
- If consensus cannot be reached, the user makes the final call.

### Estimation
When the team estimates effort:
1. Each agent estimates independently (prevents anchoring)
2. Estimates shared simultaneously
3. If estimates differ >2x → discussion round
4. Final = team median + risk buffer from highest outlier
5. Confidence: HIGH / MEDIUM / LOW always stated

## Multi-Instance Rules

| Agent | When Multiple? | Naming Convention |
|-------|----------------|-------------------|
| Rick (feature) | Parallel workflows | `rick-1`, `rick-2` or `rick-backend`, `rick-frontend` |
| Karin (fix) | Multiple independent bugs | `karin-1`, `karin-2` |
| Sanne (test) | Tests for multiple modules | `sanne-auth`, `sanne-api` |
| Role agents | Rarely >1 each | Standard name |

## Creating a New Agent

1. Copy `_template.md` to `<agent-name>.md`
2. Give the agent a name and persona
3. Define working modes, rules, and output format
4. Add to the agent table in `CLAUDE.md`
5. Commit with `feat: add <name> agent`

## Design Principles

- **Team-first** — agents collaborate, review, and reach consensus
- **Named personas** — consistent identity builds context over time
- **Role vs Task** — advisors don't implement; executors don't make architecture decisions
- **Self-improving** — every agent records lessons and detects repetition
- **Generic** — agents work across any tech stack; project specifics go in configuration sections
