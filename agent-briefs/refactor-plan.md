# Brief: Refactor Plan

**Agent:** `plan` (Thomas)
**Purpose:** Implementation plan + risk matrix for a refactor or architectural change.

## Parameters

- `{{GOAL}}` — 1-2 sentences: what we want to achieve
- `{{SCOPE}}` — modules/files affected, or "open — to be determined"
- `{{CONSTRAINTS}}` — deadlines, compat requirements, things that MUST NOT break

## Brief template

```
Design an implementation plan for: {{GOAL}}

Scope: {{SCOPE}}
Constraints: {{CONSTRAINTS}}

## Expected deliverable

A Markdown plan in `/tmp/scratch/refactor-<name>.md` containing:

### 1. Summary (1 paragraph)
What, why, which modules.

### 2. Risk matrix
| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| ... | L/M/H | L/M/H | ... |

At minimum: data-loss risk, breaking changes, performance regression, test coverage, deployment risk.

### 3. Dependency analysis
- Which modules does this touch?
- Which migrations are needed?
- Which features could regress?
- Who else should review (database-specialist? performance-engineer? security-engineer?)

### 4. Implementation steps
Numbered list of phases. Each phase: deliverable + verify-gate. Rough time-box per phase.

### 5. Open questions
Mark as `[OPEN: ...]` — where user decisions are needed. Don't assume, make it explicit.

### 6. Refinement candidates
Which role agents should review this plan before final approval? E.g.:
- `database-specialist` for schema changes
- `performance-engineer` for query/cache changes
- `security-engineer` for auth/boundary changes

## Rules

- ZERO code — this is a plan
- Time-box exploration to 2-3 minutes; start writing as soon as you know enough
- Mark uncertainties as `[OPEN]`, don't assume
- Plan goes in `/tmp/scratch/` — NOT in permanent docs until approved
```

## Refinement flow after plan

Typical sequence:

```
1. plan produces {{PLAN}} in /tmp/scratch/
2. spawn refinement (parallel):
   spawn database-specialist("review schema in {{PLAN}}")
   spawn performance-engineer("review performance in {{PLAN}}")
3. feedback gathered → SendMessage({to: "thomas", "incorporate feedback: ..."})
4. Thomas updates plan → final plan
5. user approves → spawn feature agent(s) with feature-build.md brief
```
