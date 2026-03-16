# Skill: Design Review

> **Purpose:** Evaluate architecture and design proposals for quality and fitness
> **Used by:** Architect
> **Status:** Active
> **Created:** 2026-03-16
> **Last Improved:** 2026-03-16

## When to Use

Invoke this skill when:
- A new feature requires architectural decisions
- An existing design needs to be evaluated
- The user asks "how should I structure...?" or "is this approach right?"

## Input

- Design proposal, feature requirements, or architectural question

## Procedure

### Step 1: Understand Context
1. Read existing architecture from `docs/architecture/`
2. Read existing ADRs from `docs/decisions/`
3. Understand constraints: performance, scalability, team size, timeline

### Step 2: Evaluate Fitness
1. Does the design solve the stated problem?
2. Does it fit within the existing architecture?
3. Does it introduce unnecessary complexity?
4. Does it create tight coupling or violate separation of concerns?

### Step 3: Analyze Trade-offs
1. What are the alternatives?
2. What are the pros/cons of each approach?
3. What are the long-term implications?
4. What becomes easier? What becomes harder?

### Step 4: Produce Recommendation
1. Clear recommendation with rationale
2. If the decision is significant, recommend creating an ADR
3. Identify implementation guidance for the Developer agent

### Step 5: Update Documentation (MANDATORY)
1. Update relevant `docs/architecture/` files
2. Create ADR if needed (via `skills/adr-create.md`)
3. Update `CLAUDE.md` Architecture Patterns section if new patterns emerge

## Output

- Design recommendation with rationale
- Trade-off analysis
- ADR (if significant decision)
- Implementation guidance

## Project-Specific Notes

[NOT YET CONFIGURED]

## Quality Criteria

- [ ] All alternatives considered
- [ ] Trade-offs explicitly documented
- [ ] Recommendation is clear and actionable
- [ ] Documentation updated (MANDATORY)

## Improvement Log

[No entries yet — this log grows with use]
