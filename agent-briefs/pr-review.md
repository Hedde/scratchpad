# Brief: PR Review (fan-out)

**Default agents (4-way):** `security-engineer` (Eva) + `qa-lead` (Mark) + `ux-designer` (Lisa) + `performance-engineer` (Daan) — parallel.

The blindspot this brief closes: **Daan** (performance) structurally slips out of fan-out reviews when the default is only 3 agents. Daan is now on by default — skip explicitly when not relevant.

**Optional 5th:** if your project has a `clarity-reviewer` agent (consumer-facing copy auditor), add them when the diff touches user-visible text.

## Parameters

- `{{DIFF_SCOPE}}` — `git diff main...HEAD`, specific commits, or file list
- `{{CONTEXT}}` — 2-3 sentences: what the change does and why
- `{{SKIP}}` — optional: agents to skip (see skip-policy below)

## Skip-policy (decide before spawn)

| Change | Default fan-out |
|---|---|
| Feature with UI + consumer-facing copy | **All 4** (+ clarity-reviewer if available) |
| Feature with UI but no new copy | security + qa + ux + performance |
| Pure backend / refactor | security + qa + performance (skip ux) |
| Schema/migration | security + qa + performance + Sophie via separate spawn (skip ux) |
| Bug-fix without behavior change | security + qa (skip rest) |
| Pure docs | clarity-reviewer alone (or qa if no clarity-reviewer) |
| Hot-fix | spawn `fix` directly, review afterwards |
| Diff <50 lines, docs-only | skip review, commit directly |

When in doubt: spawn the 4-way default. An extra agent costs ~500 tokens, a missed finding costs a hotfix cycle.

## Brief templates (per agent)

### Eva (security-engineer)

```
Security review of {{DIFF_SCOPE}}.

Context: {{CONTEXT}}

Focus:
- Access control (frontend + backend checks)
- Injection vectors (user input in queries, raw SQL, HTML escaping)
- Data exposure (PII in logs, API responses, error messages)
- OWASP Top 10 — full checklist

Report per finding: severity (HIGH/MED/LOW), location (file:line), concrete fix. No speculation. Vote APPROVE / CONCERN / BLOCK.

Respect the Definition of Done: docs/development/dod.md
```

### Mark (qa-lead)

```
Quality review of {{DIFF_SCOPE}}.

Context: {{CONTEXT}}

Check against docs/development/dod.md:
- Code (compile/format/lint green, no dead code)
- Tests (coverage not regressed, permission tests, happy+error paths)
- Documentation (feature-doc, inline comments where non-obvious)
- Performance basics (overlap with Daan: flag only, don't deep-dive)

Report: MUST FIX (blocks merge) vs SHOULD FIX (cleanup) vs NICE TO HAVE. Vote APPROVE / CONCERN / BLOCK.
```

### Lisa (ux-designer)

```
UX review of {{DIFF_SCOPE}}.

Context: {{CONTEXT}}

Check against docs/ui/patterns.md and existing screens:
- Screen-type pattern (list/detail/settings)
- Component consistency (buttons, forms, modals)
- Responsive behavior (mobile, tablet, desktop)
- Accessibility (keyboard, labels, contrast)

Report: check-items with status + concrete fix per deviation. Vote APPROVE / CONCERN / BLOCK.
```

### Daan (performance-engineer)

```
Performance review of {{DIFF_SCOPE}}.

Context: {{CONTEXT}}

Focus:
- N+1 queries (eager-load strategy, queries inside loops)
- Memory growth (large lists in state without pagination)
- Hot paths (request handlers running expensive work synchronously)
- Index coverage on new queries (columns in WHERE/ORDER BY)
- Caching opportunities for repeated reads

Report per finding: impact (HIGH/MED/LOW), location (file:line), concrete fix or `EXPLAIN`-style suggestion. Vote APPROVE / CONCERN / BLOCK.
```

## Orchestrator process

1. Determine fan-out via skip-policy (4/3/2 agents, +1 if clarity-reviewer applies)
2. Spawn in parallel
3. Collect reports
4. **Deduplicate findings** — same issue seen by 2 agents = 1 finding
5. **Prioritize** — MUST FIX blocks, SHOULD FIX batched, NICE TO HAVE as follow-up
6. Present to user: consolidated findings list with `file:line + severity + fix`
7. If any BLOCK vote: user decides to fix or override

## When NOT to use

- Diff <50 lines, docs-only → skip review, commit directly
- Pure refactor, behavior unchanged → Mark + Daan suffice
- Hot-fix → implement first, review after
