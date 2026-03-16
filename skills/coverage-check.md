# Skill: Coverage Check

> **Purpose:** Analyze test coverage and identify gaps
> **Used by:** Tester
> **Status:** Active
> **Created:** 2026-03-16
> **Last Improved:** 2026-03-16

## When to Use

Invoke this skill when:
- After writing tests, to verify coverage targets are met
- When assessing the overall test health of the project
- Before a release to check for coverage regressions
- The Tester agent needs to verify coverage

## Input

- (Optional) Specific files or modules to check
- Coverage targets from `docs/development/testing.md`

## Procedure

### Step 1: Run Coverage
1. Read coverage commands from `docs/development/testing.md`
2. Run the coverage tool
3. Capture the coverage report

### Step 2: Analyze
1. Compare coverage against project targets:
   - Pure functions / helpers: 90-100%
   - Business logic: 70-80%
   - UI handlers: 60-70%
2. Identify uncovered lines and branches
3. Categorize gaps by risk: which uncovered code is most dangerous?

### Step 3: Prioritize
1. High-risk gaps: business logic, security-sensitive code, error handling
2. Medium-risk gaps: integration points, edge cases
3. Low-risk gaps: simple getters, display-only code

### Step 4: Report
1. Overall coverage percentage
2. Coverage by module/component
3. Prioritized list of gaps to address
4. Recommendations for which tests to write next

### Step 5: Update Documentation (MANDATORY)
1. Update `docs/development/testing.md` with current coverage stats
2. Record improvements in this skill's log (below)

## Output

- Coverage report
- Prioritized gap analysis
- Recommendations

## Project-Specific Notes

[NOT YET CONFIGURED] — After bootstrap: coverage tool, commands, project-specific targets.

## Quality Criteria

- [ ] Coverage report generated
- [ ] Gaps identified and prioritized
- [ ] Recommendations are actionable
- [ ] Documentation updated (MANDATORY)

## Improvement Log

[No entries yet — this log grows with use]
