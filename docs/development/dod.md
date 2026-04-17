# Definition of Done

> Shared completion criteria for all tasks. Agents [MUST] reference this document instead of duplicating checklists. Skip items that don't apply to the task and note why.

## Why a shared DoD

When every agent carries its own checklist, they drift apart and duplicate effort. This file is the single source — `qa-lead`, `feature`, `fix`, and `docs-sync` all work against the same bar.

## Default criteria

### Code quality

- [ ] **[MUST]** Compiles without warnings
- [ ] **[MUST]** Formatter passes (automated via PostToolUse hook)
- [ ] **[MUST]** Linter / static analysis passes
- [ ] **[MUST]** No dead code — no commented-out blocks, no unused imports
- [ ] **[MUST]** No hardcoded values that should be configurable
- [ ] **[SHOULD]** Complexity within agreed limits per file/function

### Tests

- [ ] **[MUST]** New behavior has tests — happy path + at least one error path
- [ ] **[MUST]** Permission/authorization checks verified (frontend AND backend)
- [ ] **[SHOULD]** Coverage not regressed on touched modules
- [ ] **[SHOULD]** Integration tests for multi-layer changes

### Security

- [ ] **[MUST]** No new OWASP Top 10 exposures (injection, auth, data exposure, etc.)
- [ ] **[MUST]** Input validated at system boundaries
- [ ] **[SHOULD]** Secrets never committed (`.env`, keys)
- [ ] **[SHOULD]** New dependencies audited

### Data integrity

- [ ] **[MUST]** Migrations reversible or rollback-strategy documented
- [ ] **[MUST]** Constraints enforced (NOT NULL, UNIQUE, FK) where business logic requires
- [ ] **[SHOULD]** Backfill strategy for large tables documented

### UI & UX (when applicable)

- [ ] **[MUST]** Follows existing patterns — or new pattern documented
- [ ] **[SHOULD]** Responsive (mobile, tablet, desktop)
- [ ] **[SHOULD]** Keyboard navigation works
- [ ] **[SHOULD]** WCAG AA basics (contrast, alt-text, labels)

### Documentation

- [ ] **[MUST]** Feature doc created/updated (`docs/features/<feature>.md`)
- [ ] **[MUST]** `CLAUDE.md` reflects any new convention
- [ ] **[SHOULD]** ADR written for architectural decisions
- [ ] **[SHOULD]** Inline comment WHY (not WHAT) where non-obvious

### Commit

- [ ] **[MUST]** Scope — only task-relevant files staged
- [ ] **[MUST]** Conventional commit prefix (`feat:`, `fix:`, `chore:`, etc.)
- [ ] **[SHOULD]** Browser-verification for UI changes before commit
- [ ] **[MAY]** `[ci skip]` for docs-only commits

### Technical debt

- [ ] **[SHOULD]** New debt logged (TODO with context or issue)
- [ ] **[SHOULD]** Shortcuts commented with WHY

## Skip policy

Not every criterion applies to every change. Skip with reason:

| Change type | Typical skips |
|-------------|---------------|
| Docs-only | Code, tests, security, data integrity |
| Bug fix (no UI) | UI/UX section |
| Migration-only | UI, docs (feature-doc), ADR (unless architectural) |
| Pure refactor (behavior unchanged) | Feature-doc, tests for new behavior |
| Hot-fix | Full review; reconcile in follow-up |

When skipping, note it in the commit message or PR description. **[MUST NOT]** skip silently.

## Extending

Add project-specific items during bootstrap or after the first 2-3 features reveal what's missing. Examples:

- Framework-specific checks (e.g., tenant-prefix, telemetry registration, feature flag)
- Deployment checks (e.g., staging smoke test passed)
- Compliance checks (e.g., audit log entry for PII writes)

Keep additions above **[MUST]** / **[SHOULD]** / **[MAY]** so agents know the weight.
