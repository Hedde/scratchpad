# Skill: Code Review

> **Purpose:** Structured code review for quality, correctness, and convention adherence
> **Used by:** Reviewer
> **Status:** Active
> **Created:** 2026-03-16
> **Last Improved:** 2026-03-16

## When to Use

Invoke this skill when:
- Code has been written or modified and needs review
- A PR is being prepared
- The user asks for a code review

## Input

- Code changes (diff, files, or description of changes)

## Procedure

### Step 1: Context
1. Read `CLAUDE.md` for project conventions
2. Read `docs/development/code-organization.md` for coding patterns
3. Understand the purpose of the changes (feature doc, commit message, or user description)

### Step 2: Correctness Review
1. Does the code do what it's supposed to?
2. Are edge cases handled?
3. Are error paths covered?
4. Is the logic correct for all inputs?

### Step 3: Convention Review
1. Does the code follow project naming conventions?
2. Does it follow the project's code organization patterns?
3. Is the code formatted correctly?
4. Are imports organized per convention?

### Step 4: Quality Review
1. Is the code readable? Could a team member understand it?
2. Is it over-engineered? (Unnecessary abstractions, premature optimization)
3. Is it under-engineered? (Missing validations at system boundaries)
4. Are there performance concerns? (N+1 queries, unnecessary computation)

### Step 5: Test Review
1. Are there tests for the changes?
2. Do tests cover both happy and error paths?
3. Are tests readable and maintainable?

### Step 6: Documentation Check
1. Are all affected docs updated?
2. Does a feature doc exist (if this is a feature)?
3. Are inline comments appropriate (only where logic isn't self-evident)?

### Step 7: Provide Feedback
Format findings as:
- **Must Fix:** Issues that need to be resolved before merge
- **Should Fix:** Improvements that should be made
- **Consider:** Optional suggestions for improvement
- **Praise:** Things done well (reinforce good patterns)

## Output

- Structured review feedback
- List of identified issues by severity
- Documentation gaps found

## Project-Specific Notes

[NOT YET CONFIGURED] — After bootstrap, this will contain stack-specific review criteria.

## Quality Criteria

- [ ] All review dimensions covered
- [ ] Feedback is constructive and actionable
- [ ] Issues are categorized by severity
- [ ] Documentation gaps identified

## Improvement Log

[No entries yet — this log grows with use]
