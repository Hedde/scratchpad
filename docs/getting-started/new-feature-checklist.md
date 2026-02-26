# New Feature Checklist

Step-by-step guide for adding a new feature to the application.

> **Before starting:** Create a feature doc at `docs/features/<feature-name>.md` using the
> [feature template](../features/_template.md). This forces you to think through the design before coding.

## Phase 1 — Planning

- [ ] Create feature doc in `docs/features/<feature-name>.md`
- [ ] Define the domain: what entities, what operations?
- [ ] Sketch entity relationships (if applicable)
- [ ] Outline the user flow (how does a user interact with this?)
- [ ] Identify which existing patterns/modules are affected

**Reference:** [Code Organization](../development/code-organization.md)

## Phase 2 — Database (if applicable)

- [ ] Create migration(s) following conventions
- [ ] Create schema / model with validations
- [ ] Create service / context module with business logic
- [ ] Add any event broadcasting / hooks needed

```bash
# Create migration
[COMMAND — fill in when stack is configured]

# Run migration
[COMMAND — fill in when stack is configured]
```

**Reference:** [Database Patterns](../architecture/database.md), [Migrations](../development/migrations.md)

## Phase 3 — UI

- [ ] Create view / page / component
- [ ] Wire up data fetching (async where possible)
- [ ] Handle real-time updates (if applicable)
- [ ] Add form handling for create/update (if applicable)
- [ ] Add delete confirmation (if applicable)
- [ ] Add routing

**Reference:** [Code Organization](../development/code-organization.md), [UI Patterns](../ui/patterns.md)

## Phase 4 — Components

- [ ] Use existing design system components where possible
- [ ] Create new reusable components if patterns are shared (3+ uses)
- [ ] Follow established styling conventions

**Reference:** [UI Patterns](../ui/patterns.md)

## Phase 5 — Testing

- [ ] Write unit tests for pure functions
- [ ] Write integration tests for business logic
- [ ] Write UI tests for user interactions
- [ ] Verify coverage meets targets

```bash
# Run tests
[COMMAND — fill in when stack is configured]

# Check coverage
[COMMAND — fill in when stack is configured]
```

**Reference:** [Testing Strategy](../development/testing.md)

## Phase 6 — Cleanup & Review

- [ ] Run formatter / linter
- [ ] Run full precommit check
- [ ] Update feature doc with any decisions made during implementation
- [ ] Update other docs if patterns changed or new patterns emerged
- [ ] Commit with conventional commit message

```bash
# Format
[COMMAND — fill in when stack is configured]

# Precommit
[COMMAND — fill in when stack is configured]
```

**Reference:** [Development Workflow](../development/workflow.md)
