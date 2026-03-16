# Skill: Test Generation

> **Purpose:** Create comprehensive tests following project conventions
> **Used by:** Tester
> **Status:** Active
> **Created:** 2026-03-16
> **Last Improved:** 2026-03-16

## When to Use

Invoke this skill when:
- New code needs tests
- Test coverage is insufficient
- A regression test is needed for a bug fix

## Input

- Code to test
- Feature requirements or bug description
- Testing conventions from `docs/development/testing.md`

## Procedure

### Step 1: Analyze
1. Read `docs/development/testing.md` for test conventions
2. Identify the code's public interface (what to test)
3. List all behavior paths: happy path, error paths, edge cases, boundaries
4. Determine test type needed: unit, integration, or E2E

### Step 2: Design Tests
1. Name each test clearly: describe scenario and expected outcome
2. Follow Arrange-Act-Assert pattern
3. Group related tests logically
4. Plan test data (factories, fixtures, or inline data)

### Step 3: Write Tests
1. Write tests following project conventions
2. Cover all identified paths
3. Ensure tests are deterministic (no flakiness)
4. Keep tests fast — mock external services, not internal logic
5. One concept per test

### Step 4: Verify
1. Run the new tests — all must pass
2. Run the full test suite — nothing broken
3. Check coverage if tools are available

### Step 5: Update Documentation (MANDATORY)
1. Update `docs/development/testing.md` if new patterns were used
2. Update feature doc testing section if applicable
3. Record improvements in this skill's log (below)

## Output

- Test files following project conventions
- All tests passing
- Updated testing documentation

## Project-Specific Notes

[NOT YET CONFIGURED] — After bootstrap: test framework, commands, data strategy.

## Quality Criteria

- [ ] All behavior paths covered
- [ ] Tests are deterministic
- [ ] Tests follow project conventions
- [ ] One concept per test
- [ ] Documentation updated (MANDATORY)

## Improvement Log

[No entries yet — this log grows with use]
