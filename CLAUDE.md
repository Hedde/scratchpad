# Project Blueprint

> **This file is the AI assistant's primary context.** It triggers the right documentation for every task.
> Keep it concise — deep knowledge lives in `docs/`. This file only holds summaries and pointers.

## Bootstrap: New Project Setup

**If any section below is marked `[NOT YET CONFIGURED]`, start by interviewing the user.**

Run the bootstrap interview before writing any code:

1. Ask about the project's **purpose** (one-liner description)
2. Ask about the **tech stack** (framework, language, database, styling, deployment)
3. Ask about **development environment** (Docker, local, devcontainer, etc.)
4. Ask about **conventions** they care about (naming, git, testing, code style)
5. Ask about **deployment** target (cloud provider, CI/CD)

After each answer, immediately update the relevant `docs/` file AND this CLAUDE.md section.
Never leave a section as `[NOT YET CONFIGURED]` after learning the answer.

---

## Project Identity

- **Name:** [NOT YET CONFIGURED]
- **Description:** [NOT YET CONFIGURED]
- **Repository:** [NOT YET CONFIGURED]

## Tech Stack

[NOT YET CONFIGURED] — Run bootstrap interview.

Once configured, this section should list:
- Framework & language (with versions)
- Database
- Styling / CSS approach
- Key libraries
- Deployment target
- CI/CD

## Project Structure

[NOT YET CONFIGURED] — Will be populated after tech stack is established.

```
# This tree will be filled in as the project takes shape.
# Update it when new top-level modules/directories are added.
```

## Development

[NOT YET CONFIGURED] — See [docs/development/workflow.md](docs/development/workflow.md)

Once configured, list the 5-7 most common commands here as a quick reference.
Full command reference lives in the workflow doc.

## Conventions

> Conventions are discovered and refined over time. When a pattern is confirmed across 2+ interactions,
> document it here (summary) and in the relevant `docs/` file (detail).

### Code Style
[NOT YET CONFIGURED] — See [docs/development/code-organization.md](docs/development/code-organization.md)

### Database
[NOT YET CONFIGURED] — See [docs/architecture/database.md](docs/architecture/database.md)

### Naming
[NOT YET CONFIGURED]

### Testing
[NOT YET CONFIGURED] — See [docs/development/testing.md](docs/development/testing.md)

### Git
- Conventional commits: `feat:`, `fix:`, `chore:`, `refactor:`, `test:`, `docs:`
- See [docs/development/workflow.md](docs/development/workflow.md)

### UI & Design System
[NOT YET CONFIGURED] — See [docs/ui/patterns.md](docs/ui/patterns.md)

### Documentation
- Create `docs/features/<feature>.md` for each new feature
- Keep CLAUDE.md and docs/ up-to-date when patterns improve or mistakes are corrected
- Feature docs describe: purpose, user flows, technical decisions, and edge cases
- Record architectural decisions in `docs/decisions/`

## Architecture Patterns

> Document proven patterns here as they emerge. Link to `docs/architecture/` for deep dives.

[NOT YET CONFIGURED] — Patterns will be documented as the project evolves.

See:
- [docs/architecture/database.md](docs/architecture/database.md) — DB design & query patterns
- [docs/architecture/](docs/architecture/) — All architecture documentation

## Deployment

[NOT YET CONFIGURED] — See [docs/operations/deployment.md](docs/operations/deployment.md)

## CI/CD

[NOT YET CONFIGURED] — See [docs/operations/ci.md](docs/operations/ci.md)

## Key Domain Concepts

[NOT YET CONFIGURED] — Document domain-specific terminology and business rules here as they emerge.

---

## Documentation Map (Trigger Reference)

> **How this works:** When working on a task, Claude should consult the relevant docs below.
> Each link points to living documentation that grows with the project.

| When working on...              | Consult                                                                 |
|---------------------------------|-------------------------------------------------------------------------|
| New feature                     | [New Feature Checklist](docs/getting-started/new-feature-checklist.md)  |
| Database schema / migrations    | [Database Patterns](docs/architecture/database.md)                      |
| Architecture decisions          | [Decision Records](docs/decisions/)                                     |
| Code structure / organization   | [Code Organization](docs/development/code-organization.md)              |
| Writing tests                   | [Testing Strategy](docs/development/testing.md)                         |
| Dev commands / workflow          | [Development Workflow](docs/development/workflow.md)                     |
| UI components / styling         | [UI Patterns](docs/ui/patterns.md)                                      |
| Deployment / infrastructure     | [Deployment](docs/operations/deployment.md)                             |
| CI/CD pipeline                  | [CI/CD](docs/operations/ci.md)                                          |
| Feature specs / requirements    | [Feature Docs](docs/features/)                                          |
| Migration patterns              | [Migrations](docs/development/migrations.md)                            |

---

## Self-Learning Protocol

> **This section instructs Claude on how to evolve the project documentation.**

### When to Update Documentation

1. **New pattern discovered** — When a coding pattern works well twice, document it in the relevant `docs/` file and add a summary line to CLAUDE.md
2. **Mistake corrected** — When a wrong approach is identified, update the docs to prevent repetition. Add to `docs/decisions/` if it's architectural
3. **User preference learned** — When the user expresses a preference (style, tooling, workflow), capture it in the relevant section
4. **New feature built** — Always create `docs/features/<feature-name>.md` with purpose, flows, technical decisions, and edge cases
5. **Convention established** — When a convention is agreed upon, add it to both CLAUDE.md (summary) and the relevant doc (detail)

### How to Update

- **CLAUDE.md**: Keep summaries short (1-2 lines per item). This file should stay under 200 lines of active content
- **docs/ files**: Full detail with code examples, rationale, and edge cases
- **Replace `[NOT YET CONFIGURED]`** markers as soon as information is available
- **Never duplicate** — if information exists in a docs/ file, CLAUDE.md should only have a pointer
- **Architecture decisions** go in `docs/decisions/NNN-title.md` using the ADR template

### Interview Triggers

Ask the user for clarification when:
- A `[NOT YET CONFIGURED]` section is needed for the current task
- A docs/ file is empty and relevant to the current work
- A convention conflict is detected (code doesn't match documented patterns)
- A new technology or pattern is being introduced that isn't documented yet

### Quality Checks

Before implementing any feature, verify:
1. Is there a feature doc in `docs/features/`? If not, create one first
2. Do the architecture docs cover the patterns being used?
3. Are test patterns documented for this type of code?
4. Is the UI approach consistent with documented patterns?
