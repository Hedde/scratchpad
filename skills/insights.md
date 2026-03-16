# Skill: Insights — Periodic System Tuning

> **Purpose:** Audit and tune the agent/skill/doc system based on accumulated experience
> **Used by:** Orchestrator (via `/loop` — e.g., `/loop 30m /insights`)
> **Status:** Active
> **Created:** 2026-03-16
> **Last Improved:** 2026-03-16

## When to Use

Invoke this skill:
- **Periodically** via `/loop` (recommended: every 30-60 minutes during active development)
- After a burst of tasks (5+ completed tasks)
- When the system feels sluggish, repetitive, or misaligned
- When a new team member joins and needs a calibrated system

## Input

- The current state of all agents, skills, and docs
- Accumulated lessons learned and improvement logs

## Procedure

### Step 1: Harvest Lessons Learned

Scan all agent files for `## Lessons Learned` entries:

```
For each agent in agents/:
  - Read the Lessons Learned section
  - Group lessons by theme (pattern, mistake, efficiency, convention)
  - Identify lessons that repeat across agents (systemic issues)
```

### Step 2: Harvest Skill Improvements

Scan all skill files for `## Improvement Log` entries:

```
For each skill in skills/:
  - Read the Improvement Log
  - Identify skills that are frequently improved (hot spots)
  - Identify skills that are never used (candidates for removal)
  - Identify improvement suggestions that haven't been applied
```

### Step 3: Detect Repetitive Patterns

Check for work that's been done manually 2+ times but isn't a skill yet:

```
Sources to check:
  - Agent Lessons Learned: "I did X again" / "Same as last time"
  - Agent Improvement Backlogs: pending items
  - Skill Improvement Logs: "should have been a skill"
  - Git log: repeated commit patterns (similar messages, similar file sets)
  - Orchestrator: repeated team assembly patterns
```

For each repetitive pattern found:
1. Assess: is this worth a skill? (Will it happen again? Is it complex enough?)
2. If yes: create the skill from `skills/_template.md`
3. Assign it to the relevant agent(s)
4. Update `CLAUDE.md` skill table

### Step 4: Convention Promotion

Check for patterns that have been used 2+ times successfully:

```
Sources to check:
  - Code patterns that appear in multiple features
  - Testing patterns that work well
  - Documentation patterns that are clear and useful
  - Git commit patterns
```

For each pattern found:
1. Is it already a documented convention? → Skip
2. Is it worth promoting? → Add to `CLAUDE.md` Conventions and relevant `docs/`
3. Is it project-specific? → Add to agent/skill Project-Specific Configuration

### Step 5: Agent Performance Review

For each agent, assess:

| Dimension | Check |
|-----------|-------|
| Utilization | Is this agent being used? If never used, is it needed? |
| Accuracy | Are its lessons mostly positive or negative? |
| Skill coverage | Does it have the skills it needs? Any gaps? |
| Config completeness | Is Project-Specific Configuration filled in? |
| Improvement velocity | Are backlog items being addressed? |

Actions:
- Underused agents: consider merging or deprecating
- Overloaded agents: consider splitting into specialists
- Skill gaps: create or assign missing skills
- Stale configs: update or flag for bootstrap re-run

### Step 6: Documentation Health

Quick sweep (full audit uses `skills/doc-audit.md`):
- Count `[NOT YET CONFIGURED]` markers across all files
- Check if feature docs exist for all implemented features
- Check if ADRs exist for significant decisions
- Compare `CLAUDE.md` state to actual project state

### Step 7: Produce Insights Report

```
INSIGHTS REPORT — [DATE]
═══════════════════════════

System Health:
  Agents: [N] active, [N] with lessons, [N] with empty configs
  Skills: [N] active, [N] with improvements, [N] never used
  Docs:   [N] configured, [N] with [NOT YET CONFIGURED]

Repetitive Patterns Detected:
  → [pattern]: occurred [N] times — SKILL CREATED / PROPOSED
  → [pattern]: occurred [N] times — SKILL CREATED / PROPOSED

Conventions Promoted:
  → [pattern] promoted to convention in CLAUDE.md

Agent Tuning:
  → [agent]: [adjustment made or recommended]

Documentation Gaps:
  → [gap description]

Pending Improvements:
  → [improvement from backlog that should be prioritized]

Next Review: [recommended time]
```

### Step 8: Apply Changes

Don't just report — fix what you can:
1. Create skills for detected repetitive patterns
2. Promote confirmed conventions
3. Update agent configurations
4. Fill in resolvable `[NOT YET CONFIGURED]` markers
5. Clean up stale lessons and improvement entries

## Recommended `/loop` Configuration

```bash
# During active development (recommended)
/loop 30m /insights

# During maintenance periods
/loop 2h /insights

# After a sprint or release
/insights  (run once, thoroughly)
```

## Output

- Insights report (see template above)
- Skills created for repetitive patterns
- Conventions promoted
- Agent configurations tuned
- Documentation gaps flagged or fixed

## Quality Criteria

- [ ] All agent lessons harvested
- [ ] All skill improvement logs reviewed
- [ ] Repetitive patterns identified and addressed
- [ ] Conventions promoted where appropriate
- [ ] Agent health assessed
- [ ] Documentation gaps identified
- [ ] Actionable changes applied (not just reported)

## Improvement Log

[No entries yet — this log grows with use]
