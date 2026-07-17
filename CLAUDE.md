# Project Blueprint — Orchestrator Trigger File

> Routes every task to the right agents, skills, and docs. Self-improving: update after every completed task. Deep knowledge lives in `docs/`, agents in `agents/`, skills in `skills/`. Codex enters through `AGENTS.md`, which is a thin adapter back to this blueprint.
>
> RFC 2119 keywords: **[MUST]** = mandatory, **[SHOULD]** = recommended unless justified, **[COULD]** = optional, **[MUST NOT]** = prohibited.

---

## Critical Rules

1. **[MUST] Document after every task.** Niels runs `skills/doc-update.md`. Update CLAUDE.md, affected docs, involved agents/skills.
2. **[MUST] Self-improvement is continuous.** Every agent, skill, and doc improves itself after use — not at sprint end, not "later".
3. **[MUST] Never leave `[NOT YET CONFIGURED]` after learning the answer.** Fill in immediately.
4. **[MUST] Agents auto-improve on correction.** The corrected agent updates its own `## Gotchas` and `## Lessons Learned`.
5. **[MUST] Copy existing patterns first.** Find similar code, copy its approach. When in doubt, ask.
6. **[MUST] Server-side first.** No client-side workarounds when a server-side solution exists.
7. **[MUST] No hardcoding.** Configurable things are designed that way from the start.
8. **[SHOULD] Reuse agents and skills before adding new ones.** Prefer skills over inline procedures — check `skills/` before writing the same logic twice.
9. **[SHOULD] Minimal fix.** Bug fixes change the broken thing, not the surrounding code.
10. **[SHOULD] Not overly defensive.** Validate at boundaries; trust internal code.
11. **[SHOULD] Propose UI BEFORE implementing.** Describe in 1-2 sentences, wait for confirmation. Unknown UX pattern? Ask, don't guess.

## Output-First Workflow

- After initial orientation, state your approach in 3 bullets, then produce.
- Bug fix: diagnosis + fix proposal BEFORE scanning the codebase.
- Planning: start writing as soon as you know enough; mark unknowns as `[OPEN]`.
- Never >10 file reads without writing something. When in doubt, ask.
- **[SHOULD]** When picking up a backlog item: ask yourself if plan-review is needed before the feature agent starts — Sophie for schema impact, Daan for scale/perf impact. Refining the plan is cheaper than refining the code. No fixed threshold — decide per item.

## Session Hygiene

- Cap conversations at ~20 messages. Use `/compact` (preserves context) over `/clear` (nukes it).
- Edit the prior message instead of stacking follow-ups when correcting course.
- Cache TTL is 5 min by default — coffee break = cache miss. On paid plans, 1-hour cache pays off if you have 10+ resumes/session.
- Stop wrong-direction output immediately (Cmd+. / Esc-Esc) — output tokens are billed.
- Run `/token-audit` monthly. See [skills/token-audit.md](skills/token-audit.md).

---

## Bootstrap

If any section below is `[NOT YET CONFIGURED]`, run [skills/bootstrap-interview.md](skills/bootstrap-interview.md). It auto-detects existing vs. new projects and fills the gaps.

## Project Identity

- **Name:** [NOT YET CONFIGURED]
- **Description:** [NOT YET CONFIGURED]
- **Repository:** [NOT YET CONFIGURED]

## Tech Stack

[NOT YET CONFIGURED] — Run bootstrap.

## Project Structure

[NOT YET CONFIGURED] — Auto-populated after bootstrap.

## Conventions

Code style, database, naming, testing, UI: [NOT YET CONFIGURED] — Filled by bootstrap into `docs/development/` and `docs/ui/`.

Git: conventional commits (`feat:`, `fix:`, `chore:`, `refactor:`, `test:`, `docs:`). See [docs/development/workflow.md](docs/development/workflow.md).

## Path-Specific Rules

`.claude/rules/*.md` files load automatically when editing files matching their glob frontmatter — more efficient than inlining everything here. Bootstrap creates one rule file per stack layer (models, views, migrations, tests). See `.claude/rules/_template.md`.

## AI Tooling Adapters

`CLAUDE.md` is the canonical project blueprint. Tool-specific integration stays thin:

- `AGENTS.md` — Codex adapter and agent/runtime mapping.
- `.claude/` — Claude Code rules, settings, and native skill wrappers.
- `agents/`, `skills/`, `agent-briefs/`, and `docs/` — shared across tools.

See [docs/development/ai-tooling.md](docs/development/ai-tooling.md). Do not duplicate the persona catalog into `.agents/`; repo-root `.agents/` is reserved for Codex plugin metadata only.

## Quality Hooks

`.claude/settings.json` holds automated quality gates (PostToolUse formatter, Stop quality checks) plus the Trigger Tree statusline. The telemetry hooks themselves ship with the external `tt` plugin ([github.com/Hedde/trigger_tree](https://github.com/Hedde/trigger_tree) — log every doc read to `.trigger-tree/history.jsonl`, zero tokens); `extraKnownMarketplaces` + `enabledPlugins` in settings prompt teammates to install it. Quality gates empty until bootstrap fills them in. **Alternative:** use a git pre-commit hook instead of a Stop hook — keeps quality checks out of Claude's context and only runs at commit time.

## Architecture / Deployment / CI/CD / Domain Concepts

[NOT YET CONFIGURED] — Bootstrap and ongoing work populate `docs/architecture/`, `docs/operations/`, `docs/features/`.

---

## Agent System

Named specialists work in **teams**. Role agents advise/review; task agents plan, build, fix, test, document. The user orchestrates.

| Name | File | Type | Focus |
|------|------|------|-------|
| **Lisa** | [ux-designer.md](agents/ux-designer.md) | Role | UI consistency, accessibility |
| **Mark** | [qa-lead.md](agents/qa-lead.md) | Role | Production readiness, quality |
| **Daan** | [performance-engineer.md](agents/performance-engineer.md) | Role | Runtime performance at scale |
| **Sophie** | [database-specialist.md](agents/database-specialist.md) | Role | Schema, migrations, integrity |
| **Eva** | [security-engineer.md](agents/security-engineer.md) | Role | OWASP, access, threat modeling |
| **Thomas** | [plan.md](agents/plan.md) | Task | Implementation planning |
| **Rick** | [feature.md](agents/feature.md) | Task | Full-stack implementation |
| **Karin** | [fix.md](agents/fix.md) | Task | Root cause analysis, bug fixes |
| **Sanne** | [test.md](agents/test.md) | Task | Test strategy, coverage |
| **Niels** | [docs-sync.md](agents/docs-sync.md) | Task | Documentation sync (automatic) |

**Development lifecycle:** Plan → Build → Verify → Review → Ship. Not every task needs all phases (small bug fixes can start at Build).

For Codex: these markdown files define project personas, not registered Codex subagent types. Codex uses them as local guidance or prompt context when the user explicitly asks for delegated/parallel agent work.

| Phase | Who | Quality gate |
|-------|-----|--------------|
| Plan | Thomas | User approves plan |
| Build | Rick / Karin | Compiles without warnings |
| Verify | Sanne | Tests green, coverage adequate |
| Review | Mark + Lisa + Eva (parallel) | No BLOCKs, majority APPROVE |
| Ship | User | See [docs/development/dod.md](docs/development/dod.md) |

For team protocols (voting, consensus, multi-instance naming, parallel isolation, fan-out review patterns): see [agents/README.md](agents/README.md).

For reusable prompt templates: [agent-briefs/](agent-briefs/README.md) — saves 2–3k tokens per sprint.

## Skill System

Skills are composable procedures invoked by the orchestrator, agents, or user. Full catalog and cadence in [skills/README.md](skills/README.md).

Critical skills:
- [bootstrap-interview.md](skills/bootstrap-interview.md) — project setup (vult ook `.claude/skills/sig-audit/SKILL.md` met stack/framework-context)
- [doc-update.md](skills/doc-update.md) — **[MANDATORY]** post-task
- [token-audit.md](skills/token-audit.md) — context overhead check
- [insights.md](skills/insights.md) — periodic system tuning
- [sprint-retro.md](skills/sprint-retro.md) — post-sprint learning capture
- `tt` plugin ([github.com/Hedde/trigger_tree](https://github.com/Hedde/trigger_tree)) — `/tt status|watch|insights|help`: doc-telemetrie, untouched/dead paden, router aanscherpen. Zie [docs/features/trigger-tree.md](docs/features/trigger-tree.md).
- [.claude/skills/sig-audit/SKILL.md](.claude/skills/sig-audit/SKILL.md) — realistische SIG/TÜViT-stijl maintainability audit. **[MUST]** geconfigureerd door bootstrap met framework-context, kritieke paden en productie-gate bewijs. Audit zonder configuratie = verkeerde scores.

## Documentation

When working on a task, consult the relevant docs alongside agents/skills. Full Documentation Map (task → docs → agents → skills) in [docs/README.md](docs/README.md).

---

## Quality Framework

Inspired by ICTU Kwaliteitsaanpak and ISO 25010. Every change is evaluated across these dimensions (use judgment — not all apply to every change):

| Dimension | Who checks |
|-----------|------------|
| Correctness | Mark |
| Security | Eva |
| Performance | Daan |
| Usability + Accessibility | Lisa |
| Maintainability | Mark |
| Data integrity | Sophie |

**Definition of Done:** [docs/development/dod.md](docs/development/dod.md) — full checklist with skip-policy. Agents reference this instead of carrying their own.

**Traceability:** every requirement traceable through implementation to tests. Test descriptions reference documented behavior, not implementation details.

**Technical debt:** acceptable but visible. Log when encountered (TODO + context). Reserve ~10% of effort for debt reduction. Distinguish intentional from accidental.

---

## Self-Improvement Protocol

**[MANDATORY]** After every completed task:

1. Niels runs [skills/doc-update.md](skills/doc-update.md).
2. Update CLAUDE.md if any section was affected.
3. Every involved agent appends to `## Gotchas` and `## Lessons Learned`.
4. Every used skill appends to `## Improvement Log`.
5. Replace `[NOT YET CONFIGURED]` immediately when info is discovered.
6. New features → `docs/features/<name>.md`. Architectural decisions → `docs/decisions/NNN-title.md`.

**Triggers:**

| Event | Action | Priority |
|-------|--------|----------|
| Agent corrected | Update `## Gotchas` + `## Lessons Learned` | [MUST] |
| Task completed | Update docs, agents, skills | [MUST] |
| Repetitive task (2nd occurrence) | Propose a skill | [MUST] |
| User gives feedback | Update conventions, agent behavior | [MUST] |
| `[NOT YET CONFIGURED]` encountered | Run bootstrap or ask user | [MUST] |
| Pattern works twice | Promote to convention | [SHOULD] |
| Sprint completed | Run `skills/sprint-retro.md` | [SHOULD] |
| New tech introduced | Create/update agent + skills | [SHOULD] |

Cadence guidance and `/loop` recommendations live in [skills/README.md](skills/README.md).
