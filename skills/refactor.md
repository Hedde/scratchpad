# Skill: Refactor

> **Purpose:** Safe code restructuring without changing behavior
> **Used by:** Developer
> **Status:** Active
> **Created:** 2026-03-16
> **Last Improved:** 2026-03-16

## When to Use

Invoke this skill when:
- Code needs restructuring for clarity, performance, or maintainability
- Duplicated code needs consolidation
- Modules need splitting or merging
- Naming needs improvement

## Input

- Code to refactor and the reason for refactoring
- Architect's design (if this is a planned refactor)

## Procedure

### Step 1: Verify Safety Net
1. Ensure tests exist for the code being refactored
2. Run all tests — they must pass before refactoring
3. If tests are insufficient, write them first (use `skills/test-generate.md`)

### Step 2: Plan
1. Define the target structure
2. Break the refactoring into small, safe steps
3. Each step should leave tests passing

### Step 3: Execute
1. Make one small change at a time
2. Run tests after each change
3. Keep behavior identical — refactoring changes structure, not behavior
4. Commit after each safe step (if doing a large refactor)

### Step 4: Verify
1. Run full test suite
2. Run formatter/linter
3. Manually verify behavior (if applicable)

### Step 5: Update Documentation (MANDATORY)
1. Update `docs/development/code-organization.md` if patterns changed
2. Update `CLAUDE.md` project structure if modules changed
3. Record improvements in this skill's log (below)

## Output

- Refactored code with identical behavior
- All tests passing
- Updated documentation

## Project-Specific Notes

[NOT YET CONFIGURED]

## Quality Criteria

- [ ] Tests passed before refactoring
- [ ] Tests pass after refactoring
- [ ] Behavior is unchanged
- [ ] Code is measurably improved (readability, maintainability, or performance)
- [ ] Documentation updated (MANDATORY)

## Improvement Log

[No entries yet — this log grows with use]
