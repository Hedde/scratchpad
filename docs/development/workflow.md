# Development Workflow

> **Status:** [NOT YET CONFIGURED] — Update this file when the dev environment is set up.

## Development Environment

[Docker Compose / local install / devcontainer / nix — describe the approach]

### Prerequisites

[What needs to be installed before starting]

### Setup

```bash
# First-time setup
[COMMAND]

# Start dev server
[COMMAND]

# Stop services
[COMMAND]
```

## Common Commands

```bash
# Install dependencies
[COMMAND]

# Run dev server
[COMMAND]

# Run tests
[COMMAND]

# Format / lint code
[COMMAND]

# Database operations (if applicable)
[COMMAND] # create
[COMMAND] # migrate
[COMMAND] # reset
```

## Before Committing

**Always run before committing:**

```bash
# Format code
[COMMAND]

# Run linter (if separate from formatter)
[COMMAND]

# Run tests
[COMMAND]

# Full precommit check (if available)
[COMMAND]
```

## Commit Conventions

Use conventional commits:

```
feat: add user registration flow
fix: correct calculation in pricing module
chore: update dependencies
refactor: extract validation logic into service
test: add coverage for authentication context
docs: document deployment process
```

## Adding Dependencies

```bash
# Add a dependency
[COMMAND]

# Verify no unused dependencies
[COMMAND]
```

## Database Workflow

```bash
# Full setup from scratch
[COMMAND]

# After pulling changes with new migrations
[COMMAND]

# Start fresh (reset)
[COMMAND]

# Check migration status
[COMMAND]
```

## Debugging

### Interactive Console

```bash
[COMMAND]
```

### Debugging in Tests

[Document debugging patterns: debuggers, print statements, logging]

## Environment Variables

[Document how env vars are managed: .env files, direnv, docker-compose, etc.]

| Variable | Description | Required? |
|----------|-------------|-----------|
| [VAR] | [What it's for] | [Yes/No] |
