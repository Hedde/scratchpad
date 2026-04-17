# Brief: Feature Build

**Agent:** `feature` (Rick)
**Purpose:** Full-stack implementation of a feature, following existing patterns. Scout-first.

## Parameters

- `{{FEATURE_NAME}}` — kebab-case name, e.g. `user-profile-editor`
- `{{PLAN_REF}}` — path to implementation plan (Thomas output) or user brief
- `{{REFERENCE_BLUEPRINT}}` — existing feature/screen to copy, e.g. `users_list` for a CRUD list
- `{{ISOLATION}}` — `worktree` (parallel dev) or empty (solo)

## Brief template

```
Implement feature `{{FEATURE_NAME}}` per plan: {{PLAN_REF}}.

## Scout-first (MANDATORY)

Before building anything:
1. Grep the codebase for similar features / components
2. Reference blueprint: `{{REFERENCE_BLUEPRINT}}` — read it and copy the structure 1:1
3. Report in 2-3 lines what you found and which pattern you're copying

NEVER silently start from scratch — that's the #1 cause of rework.

## Implementation order

1. **Data layer** — schema + migration (if needed)
2. **Business logic** — context/service/model
3. **API/controller** — wire up endpoints
4. **UI** — page + form + list (follow existing pattern blueprint)
5. **Tests** — unit → integration → end-to-end per project convention
6. **Documentation** — feature doc + inline comments where non-obvious

## Definition of Done

Before declaring done: check every applicable item in `docs/development/dod.md`. Skip-policy: document what you skipped and why.

## Rules

- Formatter/compiler/lint green before saying "done"
- No backwards-compat shims or speculative abstractions
- Don't touch files outside your scope — report blockers, don't fix them
- On ambiguity: ask the user, don't guess

## Output

Final report:
- Changed files + rough LOC count
- Which DoD items touched + status
- Open questions / review points
- Follow-up suggestions
```

## Parallel build (2 developers)

If splitting the feature across 2 `feature` agents (e.g. frontend + backend):

```
rick-backend:  data layer + business logic + API
rick-frontend: UI + form + list

isolation: "worktree" for both — each on its own branch
→ await completion → merge → spawn qa-lead("review whole")
```

Split on non-overlapping files. Never two agents on the same module.
