# Skill: Implementation

> **Purpose:** Structured workflow for implementing features and code changes
> **Used by:** Developer
> **Status:** Active
> **Created:** 2026-03-16
> **Last Improved:** 2026-03-16

## When to Use

Invoke this skill when:
- A new feature needs to be built
- Existing code needs to be modified
- An implementation needs to follow a design from the Architect agent

## Input

- Feature requirements or design document
- Relevant docs from `docs/features/` and `docs/architecture/`

## Procedure

### Step 1: Pre-Flight Check
1. Read `CLAUDE.md` for project conventions
2. Check if a feature doc exists in `docs/features/`. **If not, create one from the template.**
3. Read the Architect's design (if one exists)
4. Read relevant architecture docs from `docs/architecture/`
5. Read code organization patterns from `docs/development/code-organization.md`

### Step 2: Plan
1. Break the implementation into discrete, testable units
2. Identify which existing modules/files will be modified
3. Identify which new files need to be created
4. Determine the implementation order (dependencies first)

### Step 3: Implement
1. Write code following project conventions
2. Keep changes minimal — do what's needed, nothing more
3. Follow existing patterns in the codebase
4. No security vulnerabilities (OWASP top 10)
5. No over-engineering

### Step 4: Verify
1. Run tests — all must pass
2. Run formatter/linter — code must be clean
3. Manually verify the feature works (if applicable)

### Step 5: Update Documentation (MANDATORY)
1. Update the feature doc in `docs/features/`
2. Update `CLAUDE.md` if conventions, patterns, or structure changed
3. Update code organization docs if new patterns were introduced
4. Record improvements in this skill's log (below)

## Output

- Working, tested code
- Updated feature documentation
- Clean linter/formatter output

## Project-Specific Notes

[NOT YET CONFIGURED] — After bootstrap, this will contain:
- Stack-specific implementation patterns
- Common file creation templates
- Project-specific quality checks

## Quality Criteria

- [ ] Code follows project conventions
- [ ] Tests pass
- [ ] Formatter/linter passes
- [ ] Feature doc exists and is updated
- [ ] No unnecessary complexity
- [ ] Documentation updated (MANDATORY)

## Improvement Log

[No entries yet — this log grows with use]
