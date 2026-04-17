# Agent Briefs

> Reusable prompt-templates for recurring agent tasks. The orchestrator fills in `{{PLACEHOLDERS}}` and spawns the agent. Saves 2-3k tokens per sprint vs. writing from scratch, and guarantees consistency between runs.

## Available briefs

| Brief | Purpose | Agent(s) |
|-------|---------|----------|
| [docs-audit.md](docs-audit.md) | Section-scoped documentation audit | `docs-sync` (Niels) |
| [pr-review.md](pr-review.md) | Fan-out PR review | `security-engineer` + `qa-lead` + `ux-designer` |
| [feature-build.md](feature-build.md) | Full-stack feature build with scout-first | `feature` (Rick) |
| [refactor-plan.md](refactor-plan.md) | Risk-matrix + dependency analysis | `plan` (Thomas) |

## How to use

```
1. Read the relevant brief template
2. Fill in {{PLACEHOLDERS}} with concrete scope
3. Spawn the agent with the filled-in brief as prompt
4. Collect the report
```

## When NOT to use

- One-off, unique task — write a custom brief
- Task simple enough that the agent needs no instruction
- Scope too broad for a template — split into sub-briefs

## Extending

Add a new brief when: (a) you wrote the same pattern >2×, (b) clear placeholders emerge, (c) it fits in <150 lines. Otherwise keep it a one-off.

Copy an existing brief as the starting structure. Update the README table.

## Design principles

- **Parameters on top** — explicit `{{PLACEHOLDERS}}` list before the template
- **Brief-as-prompt** — the body is the actual prompt the agent sees, not meta-instructions
- **Output contract** — every brief ends with what the agent should return
- **Project-agnostic** — templates should work for any stack; project-specifics live in agent config
