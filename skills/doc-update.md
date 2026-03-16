# Skill: Documentation Update

> **Purpose:** MANDATORY post-task documentation update across all affected files
> **Used by:** ALL agents (this is the most critical skill in the system)
> **Status:** Active
> **Created:** 2026-03-16
> **Last Improved:** 2026-03-16

## When to Use

**ALWAYS. After every task. Without exception.**

This skill is the non-negotiable final step of every workflow. No task is complete until this skill has been executed.

## Input

- Description of what was done (task, changes, decisions)
- List of files changed

## Procedure

### Step 1: Identify Affected Documentation
Based on the completed task, determine which docs need updating:

| If you changed... | Update... |
|-------------------|-----------|
| Any code | `CLAUDE.md` conventions (if patterns changed) |
| Feature code | `docs/features/<feature>.md` (create if missing) |
| Database schema | `docs/architecture/database.md`, `docs/development/migrations.md` |
| Project structure | `CLAUDE.md` Project Structure, `docs/development/code-organization.md` |
| Test patterns | `docs/development/testing.md` |
| UI components | `docs/ui/patterns.md` |
| Deployment config | `docs/operations/deployment.md` |
| CI/CD config | `docs/operations/ci.md` |
| Architecture | `docs/architecture/`, possibly `docs/decisions/` for ADR |
| Agent behavior | `agents/<name>.md` Lessons Learned section |
| Skill procedure | `skills/<name>.md` Improvement Log |
| New agent created | `CLAUDE.md` Agent table, `agents/README.md` |
| New skill created | `CLAUDE.md` Skill table, `skills/README.md` |

### Step 2: Update Each Affected Doc
For each identified doc:
1. Read the current content
2. Update with new information
3. Replace any `[NOT YET CONFIGURED]` that can now be filled
4. Remove obsolete information
5. Add code examples if new patterns were introduced

### Step 3: Update CLAUDE.md
1. Check if any summary sections need updating
2. Check if the documentation map needs new entries
3. Check if convention summaries need updating
4. Verify the agent and skill tables are current

### Step 4: Update Agent Lessons Learned
For every agent that was involved in the task:
1. Open the agent file
2. Add an entry to `## Lessons Learned`
3. Format: `- [DATE] [TASK]: [LESSON]`

### Step 5: Update Skill Improvement Logs
For every skill that was used:
1. Open the skill file
2. Add an entry to `## Improvement Log`
3. Format: `- [DATE] [CONTEXT]: [OBSERVATION] → [IMPROVEMENT]`

### Step 6: Final Sweep
Grep all docs for `[NOT YET CONFIGURED]` — fill in any that can be resolved.

## Output

- All affected documentation updated
- Agent lessons recorded
- Skill improvements logged
- `CLAUDE.md` current
- Zero resolvable `[NOT YET CONFIGURED]` markers remaining

## Project-Specific Notes

[NOT YET CONFIGURED] — After bootstrap: which docs are most critical, update frequency preferences.

## Quality Criteria

- [ ] ALL affected docs identified and updated
- [ ] `CLAUDE.md` is current
- [ ] Agent lessons are recorded
- [ ] Skill improvements are logged
- [ ] No resolvable `[NOT YET CONFIGURED]` markers remain
- [ ] No stale or obsolete information left in docs

## Improvement Log

[No entries yet — this log grows with use]
