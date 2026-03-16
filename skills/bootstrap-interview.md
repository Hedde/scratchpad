# Skill: Bootstrap Interview

> **Purpose:** Discover project identity, tech stack, conventions, and configure all docs/agents/skills
> **Used by:** Orchestrator
> **Status:** Active
> **Created:** 2026-03-16
> **Last Improved:** 2026-03-16

## When to Use

Invoke this skill when:
- The project has `[NOT YET CONFIGURED]` sections in `CLAUDE.md`
- A new project is being set up from this template
- The user asks to "set up", "bootstrap", or "configure" the project

## Input

- User availability for interview questions
- (Optional) Existing codebase to analyze

## Procedure

### Step 1: Project Identity
Ask the user:
- What is the project name?
- One-liner description — what does it do?
- Repository URL (if exists)

**Immediately update:** `CLAUDE.md` → Project Identity section

### Step 2: Tech Stack
Ask about:
- Framework & language (with versions)
- Database (type, hosting)
- Styling / CSS approach
- Key libraries and dependencies
- Deployment target (cloud, PaaS, VPS, etc.)
- CI/CD provider

**Immediately update:**
- `CLAUDE.md` → Tech Stack section
- `docs/development/workflow.md` → fill in all `[COMMAND]` placeholders
- `docs/development/testing.md` → fill in test framework and commands
- `docs/development/migrations.md` → fill in migration tool and commands
- `docs/architecture/database.md` → fill in database engine and conventions
- `docs/operations/deployment.md` → fill in platform and deployment flow
- `docs/operations/ci.md` → fill in CI provider and pipeline

### Step 3: Development Environment
Ask about:
- Local dev, Docker, devcontainer, or other
- Prerequisites for development
- Setup commands

**Immediately update:**
- `CLAUDE.md` → Development section
- `docs/development/workflow.md` → Development Environment section

### Step 4: Conventions
Ask about:
- Code style (formatter, linter, style guide)
- Naming conventions (files, modules, functions, variables)
- Testing philosophy (TDD, coverage targets, test types)
- Git conventions (beyond conventional commits)

**Immediately update:**
- `CLAUDE.md` → Conventions section (summaries)
- `docs/development/code-organization.md` → full detail
- `docs/development/testing.md` → testing conventions

### Step 5: Project Structure
Analyze the codebase (if exists) or ask the user:
- What is the directory structure?
- What are the main modules/components?

**Immediately update:**
- `CLAUDE.md` → Project Structure section
- `docs/development/code-organization.md` → Project Structure section

### Step 6: Configure Agents and Skills
Based on the tech stack, update all agent and skill files:
- Fill in `[NOT YET CONFIGURED]` in every agent's "Project-Specific Configuration"
- Fill in `[NOT YET CONFIGURED]` in every skill's "Project-Specific Notes"
- Create stack-specific agents if needed (e.g., a "Database" agent for data-heavy projects)
- Create stack-specific skills if needed (e.g., a "migration-create" skill for DB projects)

**Immediately update:**
- All agent files in `agents/`
- All skill files in `skills/`
- `CLAUDE.md` → Agent and Skill tables (if new ones were created)

### Step 7: Verify Completeness
Scan ALL files for remaining `[NOT YET CONFIGURED]` markers:
- `CLAUDE.md`
- All files in `docs/`
- All files in `agents/`
- All files in `skills/`

If any remain that could have been filled, go back and fill them.

## Output

- Fully configured `CLAUDE.md`
- All docs populated with project-specific information
- All agents configured for this tech stack
- All skills configured for this tech stack
- Zero remaining `[NOT YET CONFIGURED]` markers (that could be filled)

## Quality Criteria

- [ ] Every section of `CLAUDE.md` is filled or explicitly deferred with reason
- [ ] All `docs/` files have project-specific content
- [ ] All agents have project-specific configuration
- [ ] All skills have project-specific notes
- [ ] Development commands are verified to work
- [ ] The project structure tree is accurate

## Improvement Log

[No entries yet — this log grows with use]
