# Skill: ADR Create

> **Purpose:** Create Architecture Decision Records for significant technical decisions
> **Used by:** Architect
> **Status:** Active
> **Created:** 2026-03-16
> **Last Improved:** 2026-03-16

## When to Use

Invoke this skill when:
- A significant architectural or technical decision is made
- A technology choice needs to be documented
- A design trade-off was explicitly evaluated
- The Architect agent recommends recording a decision

## Input

- The decision context: what problem was being solved?
- The options considered
- The decision made and rationale

## Procedure

### Step 1: Determine ADR Number
1. Check `docs/decisions/` for existing ADRs
2. Use the next sequential number (e.g., `001`, `002`, etc.)

### Step 2: Create ADR File
1. Copy `docs/decisions/_template.md` to `docs/decisions/NNN-title.md`
2. Use a descriptive, lowercase-hyphenated title

### Step 3: Fill in ADR
1. **Status:** Set to "Accepted" (or "Proposed" if still under discussion)
2. **Date:** Today's date
3. **Context:** Why this decision was needed
4. **Options Considered:** List all alternatives with pros/cons
5. **Decision:** What was chosen and why
6. **Consequences:** Positive, negative, and neutral impacts

### Step 4: Cross-Reference
1. Update relevant `docs/architecture/` files to reference the ADR
2. Update `CLAUDE.md` Architecture Patterns section if applicable
3. If this ADR supersedes another, update the old ADR's status

## Output

- New ADR file in `docs/decisions/`
- Cross-references updated

## Project-Specific Notes

[NOT YET CONFIGURED]

## Quality Criteria

- [ ] ADR is complete (no empty sections)
- [ ] All alternatives are documented
- [ ] Rationale is clear
- [ ] Cross-references are updated
- [ ] Old ADRs are updated if superseded

## Improvement Log

[No entries yet — this log grows with use]
