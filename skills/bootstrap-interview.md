# Skill: Bootstrap — Auto-Discovery & Configuration

> **Purpose:** Detect project type (existing vs new), discover what's there, fill in the gaps via decisions with the user
> **Used by:** Orchestrator
> **Status:** Active
> **Created:** 2026-03-16
> **Last Improved:** 2026-03-16

## When to Use

Invoke this skill when:
- The project has `[NOT YET CONFIGURED]` sections in `CLAUDE.md`
- This template is added to an existing or new project
- The user asks to "set up", "bootstrap", or "configure" the project

## Input

- The project directory (codebase, if any)
- User availability for decision questions

## Procedure

### Step 0: Detect Project Type

**This is the critical first step.** Determine if this is an existing or new project:

```
Scan the project directory for NON-template files:
  - Source code files (*.ex, *.py, *.ts, *.go, *.rs, *.rb, *.java, etc.)
  - Package manifests (mix.exs, package.json, Cargo.toml, go.mod, Gemfile, pom.xml, pyproject.toml, requirements.txt, etc.)
  - Config files (docker-compose.yml, .env.example, Dockerfile, etc.)
  - CI/CD configs (.github/workflows/, .gitlab-ci.yml, etc.)
  - Database files (schema.rb, priv/repo/migrations/, alembic/, etc.)
  - Any file NOT in docs/, agents/, skills/, or CLAUDE.md
```

**Decision:**
- **Files found → EXISTING PROJECT** — Go to Step 1A (Discovery-first)
- **No files found → NEW PROJECT** — Go to Step 1B (Decisions-first)

---

### PATH A: Existing Project (Discovery-First)

> Philosophy: scan everything first, present findings, only ask about what can't be discovered.

#### Step 1A: Auto-Discover Tech Stack

Scan and analyze (do NOT ask the user yet):

| What to Detect | Where to Look |
|---------------|--------------|
| Language & framework | Package manifests, file extensions, imports |
| Framework version | Lock files, version pins in manifests |
| Database | Config files, ORM/schema files, docker-compose services |
| Test framework | Test directories, test config, package manifest dev-deps |
| Linter/formatter | Config files (`.eslintrc`, `.prettierrc`, `mix.exs`, `ruff.toml`, etc.) |
| CI/CD | `.github/workflows/`, `.gitlab-ci.yml`, `Jenkinsfile`, etc. |
| Deployment | `Dockerfile`, `fly.toml`, `render.yaml`, `vercel.json`, `Procfile`, etc. |
| Styling/CSS | Tailwind config, PostCSS, CSS-in-JS imports, stylesheet files |
| Key libraries | Dependencies in manifest, imports in source code |
| Dev environment | `docker-compose.yml`, `.devcontainer/`, `flake.nix`, `Makefile` |

#### Step 2A: Auto-Discover Project Structure

```
- Map the directory tree (top 3 levels)
- Identify main modules, components, or packages
- Identify test structure and how it mirrors source
- Identify config vs. source vs. generated directories
```

#### Step 3A: Auto-Discover Conventions

Analyze actual code for patterns (do NOT ask yet):

| What to Detect | How |
|---------------|-----|
| Naming conventions | Sample file names, function names, variable names |
| Code organization | Module structure, layering, separation of concerns |
| Test patterns | Test file structure, helper usage, assertion style |
| Git conventions | Read recent commit messages from `git log` |
| Import ordering | Read top of source files for import patterns |
| Error handling | Scan for error handling patterns in source |

#### Step 4A: Present Findings to User

**This is the critical decision step.** Present ALL discoveries as a structured report:

```
DISCOVERY REPORT
════════════════

Project: [detected name from manifest/git/directory]
Description: [inferred from README, manifest description, or "needs your input"]

Tech Stack (discovered):
  ✓ Language: [detected] [version]
  ✓ Framework: [detected] [version]
  ✓ Database: [detected]
  ✓ Test framework: [detected]
  ✓ Linter/formatter: [detected]
  ✓ CI/CD: [detected]
  ✓ Deployment: [detected]
  ? Styling: [detected or "not found — what do you use?"]
  ? [anything unclear]

Project Structure (discovered):
  [directory tree]

Conventions (observed):
  ✓ Naming: [observed pattern]
  ✓ Git commits: [observed pattern]
  ✓ Code organization: [observed pattern]
  ? Testing philosophy: [observed or "unclear — what's your approach?"]

Items needing your input:
  1. [thing that couldn't be discovered]
  2. [thing that was ambiguous]
  3. [description — what does this project do?]

Does this look correct? What should I change or add?
```

#### Step 5A: Process User Corrections & Fill Gaps

1. Apply any corrections the user provides
2. Ask targeted questions ONLY for items marked with `?`
3. **Immediately update** all docs, agents, and skills with confirmed information (see update targets below)

#### Step 6A: Discover Commands

Try to detect runnable commands:

| Command Type | Where to Find |
|-------------|--------------|
| Dev server | `package.json` scripts, `Makefile`, `Procfile`, README |
| Tests | `package.json` scripts, `mix.exs` aliases, `Makefile`, README |
| Linting | `package.json` scripts, `Makefile`, pre-commit config |
| Database | `package.json` scripts, `mix.exs` aliases, `Makefile` |
| Build | `package.json` scripts, `Makefile`, `Dockerfile` |

**Present to user:** "I found these commands — are they correct?"

**Immediately update:** `docs/development/workflow.md` with confirmed commands.

---

### PATH B: New Project (Decisions-First)

> Philosophy: nothing to discover, so ask the user for all decisions upfront.

#### Step 1B: Project Identity
Ask the user:
- What is the project name?
- One-liner description — what does it do?
- Repository URL (if exists)

**Immediately update:** `CLAUDE.md` → Project Identity section

#### Step 2B: Tech Stack Decisions
Ask about:
- Language & framework (with preferred versions)
- Database (type, hosting)
- Styling / CSS approach (if web project)
- Key libraries they want to use
- Deployment target (cloud, PaaS, VPS, etc.)
- CI/CD provider

**Immediately update:** all docs (see update targets below)

#### Step 3B: Development Environment Decisions
Ask about:
- Local dev, Docker, devcontainer, or other
- Prerequisites for development
- Setup commands they want to use

**Immediately update:** `docs/development/workflow.md`

#### Step 4B: Convention Decisions
Ask about:
- Code style (formatter, linter, style guide)
- Naming conventions (files, modules, functions, variables)
- Testing philosophy (TDD, coverage targets, test types)
- Git conventions (beyond conventional commits)

**Immediately update:** `CLAUDE.md` conventions + `docs/development/`

#### Step 5B: Initial Structure
Ask about or propose:
- What directory structure do they want?
- What are the main modules/components?
- Propose a structure based on chosen tech stack

**Immediately update:** `CLAUDE.md` → Project Structure, `docs/development/code-organization.md`

---

### Step 7: Configure Agents and Skills (Both Paths)

Based on the (discovered or decided) tech stack, update all agent and skill files:
- Fill in `[NOT YET CONFIGURED]` in every agent's "Project-Specific Configuration"
- Fill in `[NOT YET CONFIGURED]` in every skill's "Project-Specific Notes"
- Create stack-specific agents if needed (e.g., a "Database" agent for data-heavy projects)
- Create stack-specific skills if needed (e.g., a "migration-create" skill for DB projects)

**Immediately update:**
- All agent files in `agents/`
- All skill files in `skills/`
- `CLAUDE.md` → Agent and Skill tables (if new ones were created)

### Step 8: Verify Completeness

Scan ALL files for remaining `[NOT YET CONFIGURED]` markers:
- `CLAUDE.md`
- All files in `docs/`
- All files in `agents/`
- All files in `skills/`

If any remain that could have been filled, go back and fill them.

---

## Update Targets Reference

When updating, hit ALL of these:

| Information | Update These Files |
|------------|-------------------|
| Project name, description | `CLAUDE.md` → Project Identity |
| Tech stack | `CLAUDE.md` → Tech Stack |
| Framework & language | `docs/development/workflow.md`, `docs/development/code-organization.md` |
| Database | `docs/architecture/database.md`, `docs/development/migrations.md` |
| Test framework | `docs/development/testing.md` |
| CI/CD | `docs/operations/ci.md` |
| Deployment | `docs/operations/deployment.md` |
| UI/Styling | `docs/ui/patterns.md` |
| Commands | `docs/development/workflow.md` (fill in all `[COMMAND]` placeholders) |
| Project structure | `CLAUDE.md` → Project Structure, `docs/development/code-organization.md` |
| Conventions | `CLAUDE.md` → Conventions, `docs/development/code-organization.md` |
| Agent config | All files in `agents/` → Project-Specific Configuration |
| Skill config | All files in `skills/` → Project-Specific Notes |

## Output

- Fully configured `CLAUDE.md`
- All docs populated with project-specific information
- All agents configured for this tech stack
- All skills configured for this tech stack
- Zero remaining `[NOT YET CONFIGURED]` markers (that could be filled)

## Quality Criteria

- [ ] Project type correctly detected (existing vs new)
- [ ] For existing projects: discoveries presented before questions asked
- [ ] For new projects: decisions gathered systematically
- [ ] User has confirmed or corrected all findings/decisions
- [ ] Every section of `CLAUDE.md` is filled or explicitly deferred with reason
- [ ] All `docs/` files have project-specific content
- [ ] All agents have project-specific configuration
- [ ] All skills have project-specific notes
- [ ] Development commands are verified to work
- [ ] The project structure tree is accurate

## Improvement Log

[No entries yet — this log grows with use]
