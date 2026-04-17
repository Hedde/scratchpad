# Brief: PR Review (fan-out)

**Agents:** `security-engineer` (Eva) + `qa-lead` (Mark) + `ux-designer` (Lisa) — parallel
**Purpose:** Three-perspective review of a diff or branch.

## Parameters

- `{{DIFF_SCOPE}}` — `git diff main...HEAD`, specific commits, or file list
- `{{CONTEXT}}` — 2-3 sentences: what the change does and why
- `{{SKIP}}` — optional agents to skip (`ux` if no UI, `security` for pure docs)

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
- Performance (obvious N+1, unnecessary computation)

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

## Orchestrator process

1. Spawn 3 agents in parallel (or 2 if `{{SKIP}}` includes one)
2. Collect 3 reports
3. **Deduplicate findings** — same issue seen by 2 agents = 1 finding
4. **Prioritize** — MUST FIX blocks, SHOULD FIX batched, NICE TO HAVE as follow-up
5. Present to user: consolidated findings list with `file:line + severity + fix`
6. If any BLOCK vote: user decides to fix or override

## When NOT to use

- Diff <50 lines, docs-only → skip review, commit directly
- Pure refactor, behavior unchanged → Mark alone suffices
- Hot-fix → implement first, review after
