# Skill: Sprint Retro

> **Purpose:** Immediate reflection after a completed sprint or audit. Extracts lessons and proposes which should become permanent rules.
> **Used by:** User (orchestrator), invoked as `/sprint-retro`
> **Status:** Active
> **Created:** 2026-04-17
> **Last Improved:** 2026-04-17

## When to Use

Invoke this skill:
- After a multi-agent sprint (build + review)
- After a large audit session
- When the user says "what did we learn" or "retro this"
- At the end of a long session with multiple course corrections

**Difference from `insights.md`:** `sprint-retro` is focused on a just-completed sprint (fresh signal). `insights` is periodic system-wide tuning (accumulated signal). Run retro immediately; run insights every few hours.

## When NOT to Use

- After a trivial single-step task (no pattern)
- During active work (wait until something's finished)
- Sessions with <10 tool calls (not enough signal)

## Input

- The session context (recent messages, tool calls, agent reports)
- Optional: user-stated framing ("this sprint was about X")

## Procedure

### Step 1: Scope

Ask the user (or infer):
- Which sprint/audit just completed?
- Was it build, review, audit, bugfix, refactor?
- How many agents involved?

### Step 2: Scan for learning signals

Look for these signals in the session:

| Signal | Points to |
|--------|-----------|
| User corrected an approach ("not that, but this") | → feedback-type lesson |
| User confirmed a non-obvious choice ("yes, exactly") | → feedback-type lesson (validated judgment) |
| Unexpected gotcha in codebase | → gotcha for an agent file or project docs |
| New pattern/agreement not in docs | → candidate convention for CLAUDE.md or docs |
| Status change on a tracked item | → update to docs or project log |
| New infrastructure/tooling detail | → project-context note |

### Step 3: Formulate proposals

Per signal: draft a concrete memory/doc entry. Format varies by type:

**Agent gotcha:**
```markdown
## Gotchas
- **[TITLE]** — [what goes wrong] → [correct approach]. Discovered: YYYY-MM-DD
```

**Convention for CLAUDE.md:**
```markdown
### [Category]
- **[Rule]** — [rationale]. When to apply: [context]
```

**Lesson learned (agent file):**
```markdown
## Lessons Learned
- YYYY-MM-DD [TASK]: [what worked / what didn't / what to do differently]
```

### Step 4: Present to user

Report in one message:

```markdown
## Sprint Retro — <date + scope>

### Learning signals detected

1. **<title>** (type: agent-gotcha | convention | lesson)
   - Signal: <where you saw it>
   - Proposed entry:
     ```
     <full draft>
     ```
   - Target: <file path>
   - Save? [yes / no / modify]

2. ...

### Documentation gaps

- `docs/X.md`: <suggestion>

### Nothing new detected
(if applicable)
```

### Step 5: Apply on user approval

- Write approved entries to target files
- Update `CLAUDE.md` if a convention is promoted
- For doc gaps: delegate to `docs-sync` agent or let the user decide

## Rules

- **[MUST NOT]** silently save — user always approves
- **[MUST NOT]** overwrite existing entries without a merge proposal
- **[MUST]** cap at 5 signals per retro — if more, ask which 5 matter most
- **[MUST]** proposals are actionable — "be careful" is not a lesson, "NEVER X without Y" is
- **[MUST]** skip obvious stuff — anything already in CLAUDE.md or existing gotcha lists

## Output

- Per-signal proposal list
- Applied entries (on user approval)
- Updated `CLAUDE.md` if conventions promoted

## Quality Criteria

- [ ] At least one concrete signal surfaced (or explicit "nothing new")
- [ ] Every proposal is actionable and has a target file
- [ ] User approved before any writes
- [ ] Nothing duplicates existing content

## Improvement Log

[No entries yet — this log grows with use]
