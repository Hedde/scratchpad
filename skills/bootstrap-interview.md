# Skill: Bootstrap — Auto-Discovery & Configuration

> **Purpose:** Detect project type (existing vs new), discover what's there, fill in the gaps via decisions with the user
> **Used by:** User (orchestrator)
> **Status:** Active
> **Created:** 2026-03-16
> **Last Improved:** 2026-04-07

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

> **[MUST]** — This is the critical first step. Never skip detection.

Scan the project directory for NON-template files:

```
Source code files (*.py, *.ts, *.go, *.rs, *.rb, *.java, *.ex, *.cs, etc.)
Package manifests (package.json, Cargo.toml, go.mod, Gemfile, pom.xml, pyproject.toml, etc.)
Config files (docker-compose.yml, .env.example, Dockerfile, etc.)
CI/CD configs (.github/workflows/, .gitlab-ci.yml, etc.)
Database files (migrations/, schema files, etc.)
Any file NOT in docs/, agents/, skills/, or CLAUDE.md
```

**Decision:**
- **Files found → EXISTING PROJECT** — Go to Path A (Discovery-first)
- **No files found → NEW PROJECT** — Go to Path B (Decisions-first)

---

### PATH A: Existing Project (Discovery-First)

> Philosophy: scan everything first, present findings, only ask about what can't be discovered.

#### Step 1A: [MUST] Auto-Discover Tech Stack

Scan and analyze — do NOT ask the user yet:

| What to Detect | Where to Look |
|---------------|--------------|
| Language & framework | Package manifests, file extensions, imports |
| Framework version | Lock files, version pins in manifests |
| Database | Config files, ORM/schema files, docker-compose services |
| Test framework | Test directories, test config, dev-dependencies |
| Linter/formatter | Config files (`.eslintrc`, `.prettierrc`, `ruff.toml`, `biome.json`, etc.) |
| CI/CD | `.github/workflows/`, `.gitlab-ci.yml`, `Jenkinsfile`, etc. |
| Deployment | `Dockerfile`, `fly.toml`, `render.yaml`, `vercel.json`, `Procfile`, etc. |
| Styling/CSS | Tailwind config, PostCSS, CSS-in-JS imports, stylesheet files |
| Key libraries | Dependencies in manifest, imports in source code |
| Dev environment | `docker-compose.yml`, `.devcontainer/`, `flake.nix`, `Makefile` |
| Coding standards | Linter/formatter configs, `.editorconfig`, pre-commit hooks |

#### Step 2A: [MUST] Auto-Discover Project Structure

```
- Map the directory tree (top 3 levels)
- Identify main modules, components, or packages
- Identify test structure and how it mirrors source
- Identify config vs. source vs. generated directories
```

#### Step 3A: [MUST] Auto-Discover Conventions

Analyze actual code for patterns — do NOT ask yet:

| What to Detect | How |
|---------------|-----|
| Naming conventions | Sample file names, function names, variable names |
| Code organization | Module structure, layering, separation of concerns |
| Test patterns | Test file structure, helper usage, assertion style |
| Git conventions | Read recent commit messages from `git log --oneline -20` |
| Import ordering | Read top of source files for import patterns |
| Error handling | Scan for error handling patterns in source |
| Coding standards | Parse linter/formatter config for enforced rules |

#### Step 4A: [MUST] Auto-Discover Commands

Detect runnable commands before presenting findings:

| Command Type | Where to Find |
|-------------|--------------|
| Dev server | `package.json` scripts, `Makefile`, `Procfile`, README |
| Tests | `package.json` scripts, `Makefile`, README, CI config |
| Linting/formatting | `package.json` scripts, `Makefile`, pre-commit config |
| Database | `package.json` scripts, `Makefile`, README |
| Build | `package.json` scripts, `Makefile`, `Dockerfile`, CI config |

#### Step 5A: [MUST] Present Discovery Report

Present ALL discoveries as a structured report:

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

Commands (discovered):
  ✓ Dev server: [command]
  ✓ Tests: [command]
  ✓ Lint/format: [command]
  ? [any unclear]

Coding Standards (from config):
  ✓ [rules detected from linter/formatter configs]

Project Structure:
  [directory tree, top 3 levels]

Conventions (observed):
  ✓ Naming: [observed pattern]
  ✓ Git commits: [observed pattern]
  ✓ Code organization: [observed pattern]
  ? Testing philosophy: [observed or "unclear — what's your approach?"]

Items needing your input:
  1. [thing that couldn't be discovered]
  2. [thing that was ambiguous]

Does this look correct? What should I change or add?
```

#### Step 6A: [MUST] Process User Corrections

1. Apply any corrections the user provides
2. Ask targeted questions ONLY for items marked with `?`
3. **[MUST]** immediately update all docs, agents, and skills (see Update Targets)

#### Step 7A: [SHOULD] Discover Workflow Patterns

Ask the user about recurring tasks and workflows:
- "What tasks do you do repeatedly that could become skills?"
- "Are there safety checks or validation steps you always run?"
- "What are common gotchas new developers hit in this codebase?"

Create skills for any patterns identified.

---

### PATH B: New Project (Decisions-First)

> Philosophy: nothing to discover, so gather all decisions upfront.

#### Step 1B: [MUST] Project Identity
Ask the user:
- What is the project name?
- One-liner description — what does it do?
- Repository URL (if exists)

**[MUST]** immediately update: `CLAUDE.md` → Project Identity section

#### Step 2B: [MUST] Tech Stack Decisions
Ask about:
- Language & framework (with preferred versions)
- Database (type, hosting)
- Styling / CSS approach (if web project)
- Key libraries they want to use
- Deployment target (cloud, PaaS, VPS, etc.)
- CI/CD provider

**[MUST]** immediately update: all docs (see Update Targets)

#### Step 3B: [MUST] Development Environment Decisions
Ask about:
- Local dev, Docker, devcontainer, or other
- Prerequisites for development
- Setup commands they want to use

**[MUST]** immediately update: `docs/development/workflow.md`

#### Step 4B: [SHOULD] Convention Decisions
Ask about:
- Code style (formatter, linter, style guide)
- Naming conventions (files, modules, functions, variables)
- Testing philosophy (TDD, coverage targets, test types)
- Git conventions (beyond conventional commits)

**[MUST]** immediately update: `CLAUDE.md` conventions + `docs/development/`

#### Step 5B: [SHOULD] Initial Structure
Ask about or propose:
- What directory structure do they want?
- What are the main modules/components?
- Propose a structure based on chosen tech stack

**[MUST]** immediately update: `CLAUDE.md` → Project Structure, `docs/development/code-organization.md`

---

### Step 8: [MUST] Configure Agents (Both Paths)

Based on the (discovered or decided) tech stack, update all agent files:

1. **[MUST]** Fill in `[NOT YET CONFIGURED]` in every agent's "Project-Specific Configuration":
   - **Lisa (UX):** UI framework, component library, design system, breakpoints
   - **Mark (QA):** Test commands, linting commands, quality thresholds
   - **Daan (Performance):** Expected load profile, database engine, caching tools
   - **Sophie (Database):** Database engine, ORM, migration tool, naming conventions
   - **Eva (Security):** Auth framework, session mechanism, deployment security
   - **Thomas (Plan):** Key architecture patterns, common file locations
   - **Rick (Dev):** Tech stack, framework patterns, coding conventions, test commands
   - **Karin (Fix):** Common bug patterns, known gotchas, test commands
   - **Sanne (Test):** Test framework, test commands, coverage tools, factory patterns
   - **Niels (Docs):** Documentation structure, style guide, doc locations

2. **[SHOULD]** Fill in `[NOT YET CONFIGURED]` in every skill's "Project-Specific Notes"

3. **[COULD]** Create stack-specific skills if needed

### Step 9: [MUST] Verify Completeness

Scan ALL files for remaining `[NOT YET CONFIGURED]` markers:
- `CLAUDE.md`
- All files in `docs/`
- All files in `agents/`
- All files in `skills/`

If any remain that **[COULD]** have been filled, go back and fill them.

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
- [ ] For existing projects: coding standards extracted from config files
- [ ] For new projects: decisions gathered systematically
- [ ] User has confirmed or corrected all findings/decisions
- [ ] Every section of `CLAUDE.md` is filled or explicitly deferred with reason
- [ ] All `docs/` files have project-specific content
- [ ] All 10 agents have project-specific configuration
- [ ] All skills have project-specific notes
- [ ] Development commands are verified to work
- [ ] Workflow patterns discovered and codified as skills

## Improvement Log

- 2026-04-07: Added coding standards detection from config files (inspired by /init), added workflow pattern discovery step, added explicit agent configuration per-name, added RFC keywords throughout
