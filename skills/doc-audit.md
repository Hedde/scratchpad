# Skill: Documentation Audit

> **Purpose:** Periodic health check of all project documentation
> **Used by:** Documenter
> **Status:** Active
> **Created:** 2026-03-16
> **Last Improved:** 2026-03-16

## When to Use

Invoke this skill when:
- A periodic documentation check is requested
- The project feels like its docs have drifted from reality
- Before a major release or milestone
- When onboarding a new team member

## Input

- (None required — this skill audits everything)

## Procedure

### Step 1: Scan for Completeness
Check every documentation file for:
1. `[NOT YET CONFIGURED]` markers — can any be filled now?
2. `[COMMAND]` placeholders — are commands documented?
3. `[TODO]` markers — are there outstanding items?
4. Empty sections — should they have content?

### Step 2: Check Accuracy
For each doc, verify:
1. Does the documented structure match the actual codebase?
2. Do documented commands actually work?
3. Do documented conventions match the actual code?
4. Are documented patterns still in use?

### Step 3: Check Coverage
1. Does every feature have a doc in `docs/features/`?
2. Do all architectural decisions have ADRs?
3. Is `CLAUDE.md` up to date?
4. Are agent and skill tables current?
5. Are there undocumented patterns in the code?

### Step 4: Produce Report
Generate a documentation health report:
- **Complete:** Docs that are accurate and current
- **Needs Update:** Docs with stale or inaccurate information
- **Missing:** Documentation that should exist but doesn't
- **Obsolete:** Documentation that should be removed

### Step 5: Fix Issues
Address findings immediately:
1. Update stale docs
2. Create missing docs
3. Remove obsolete docs
4. Fill in resolvable placeholders

## Output

- Documentation health report
- All fixable issues resolved
- List of issues that need user input

## Project-Specific Notes

[NOT YET CONFIGURED]

## Quality Criteria

- [ ] All docs scanned
- [ ] Accuracy verified against codebase
- [ ] Coverage gaps identified
- [ ] Fixable issues resolved
- [ ] Report produced

## Improvement Log

[No entries yet — this log grows with use]
