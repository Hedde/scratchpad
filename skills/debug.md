# Skill: Debug

> **Purpose:** Systematic debugging process to find and fix root causes
> **Used by:** Developer
> **Status:** Active
> **Created:** 2026-03-16
> **Last Improved:** 2026-03-16

## When to Use

Invoke this skill when:
- A bug needs to be investigated
- Code is behaving unexpectedly
- An error or failure needs root cause analysis

## Input

- Bug description, error message, or unexpected behavior
- Steps to reproduce (if available)

## Procedure

### Step 1: Reproduce
1. Understand the expected behavior
2. Understand the actual behavior
3. Find reliable reproduction steps
4. Identify the minimal reproduction case

### Step 2: Isolate
1. Where does the bug manifest? (UI, API, database, etc.)
2. Trace the data flow from input to output
3. Narrow down to the specific module/function
4. Check recent changes (git log) for likely culprits

### Step 3: Diagnose
1. Read the relevant code carefully
2. Check for common causes: off-by-one, null handling, type mismatches, race conditions
3. Add targeted logging or debugging if needed
4. Form a hypothesis about the root cause

### Step 4: Fix
1. Write the minimal fix for the root cause (not a symptom)
2. Verify the fix resolves the issue
3. Ensure no regressions

### Step 5: Prevent
1. Write a regression test that would have caught this bug
2. If the bug reveals a pattern gap, document it

### Step 6: Update Documentation (MANDATORY)
1. If the bug reveals a common pitfall, add it to relevant docs
2. Update agent lessons learned
3. Record improvements in this skill's log (below)

## Output

- Root cause identified and fixed
- Regression test written
- Updated documentation (if pattern gap found)

## Project-Specific Notes

[NOT YET CONFIGURED] — After bootstrap: debugging tools, logging setup, common error patterns.

## Quality Criteria

- [ ] Root cause identified (not just symptom fixed)
- [ ] Regression test written
- [ ] No new issues introduced
- [ ] Documentation updated (MANDATORY)

## Improvement Log

[No entries yet — this log grows with use]
