# Testing Strategy

> **Status:** [NOT YET CONFIGURED] — Update this file when the test framework and conventions are established.

## Test Framework

[Specify: Jest, ExUnit, pytest, RSpec, etc.]

## Test Types

| Type | Database? | Parallel? | Purpose |
|------|-----------|-----------|---------|
| Unit | No | Yes | Pure functions, transformations |
| Integration | Yes | Varies | Service/context modules, DB operations |
| E2E / UI | Yes | No | Full user flows, browser interactions |

## Commands

```bash
# Run all tests
[COMMAND]

# Run with coverage
[COMMAND]

# Run specific test file
[COMMAND]

# Run specific test by name/line
[COMMAND]

# Run only a test category
[COMMAND]
```

## Test Structure

```
# Mirror source structure:
test/
  [mirrors lib/ or src/ structure]
  support/            # Test helpers, fixtures, factories
```

## Writing Tests

### Unit Tests

```
# Example unit test
```

### Integration Tests

```
# Example integration test
```

### UI / LiveView / Component Tests

```
# Example UI test
```

## Test Data

[How to create test data: factories, fixtures, seeds, builders?]

```
# Example
```

## Coverage

### Configuration

[Coverage tool and configuration]

### Targets

| Layer | Target |
|-------|--------|
| Pure functions / helpers | 90-100% |
| Business logic | 70-80% |
| UI handlers | 60-70% |

### Checking Coverage

```bash
# Generate coverage report
[COMMAND]
```

## Best Practices

- Prefer parallel test execution where possible
- Test both success and error paths
- Test validations explicitly
- Use descriptive test names that explain the scenario
- Keep tests focused: one assertion per concept
- Run full suite before pushing
