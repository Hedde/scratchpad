# Codex Adapter — Project Blueprint

This file is the Codex entry point. It intentionally stays small to prevent drift.

## Canonical Sources

1. Read `CLAUDE.md` as the canonical project blueprint for rules, quality gates, agents, skills, and documentation flow.
2. Use `docs/` for durable project knowledge.
3. Use `agents/` as reusable specialist persona definitions.
4. Use `skills/` as local procedural playbooks.
5. Use `agent-briefs/` as reusable prompt templates.

If this file conflicts with `CLAUDE.md`, follow `CLAUDE.md` for project policy and update this adapter only when the Codex integration itself changed.

## Codex Execution Rules

- Apply the blueprint directly unless the user is only asking for analysis or planning.
- Prefer local repository conventions over generic Codex defaults.
- Before code changes, inspect the relevant docs, agent persona, and skill for the task.
- After completed work, run the same documentation sync expectation as the blueprint: update affected docs and conventions. If project state changed, update `CLAUDE.md`; if Codex-specific behavior changed, update this file too.
- Do not duplicate long rules from `CLAUDE.md` here.

## Agent Folder Convention

`agents/` is the cross-tool catalog of named project specialists. It is not a Codex subagent registration directory.

Codex subagents are tool/runtime capabilities. Use them only when the user explicitly asks for delegation or parallel agent work, then map the requested project persona to the closest Codex role:

| Project persona | Codex usage |
|-----------------|-------------|
| Thomas / Mark / Lisa / Eva / Sophie / Daan | Use as instructions for local analysis, or as a bounded `explorer` task when explicit delegation is requested |
| Rick / Karin / Sanne / Niels | Use as local workflow guidance, or as a bounded `worker` task with disjoint file ownership when explicit delegation is requested |

When spawning a Codex subagent, include the relevant `agents/<name>.md` content or a concise summary in the prompt. Do not invent a `subagent_type` from the markdown filename.

## `.agents/` Convention

Reserve repo-root `.agents/` for Codex plugin marketplace metadata only, such as `.agents/plugins/marketplace.json`, if this template later ships plugins. Do not mirror the `agents/` persona catalog into `.agents/`; that creates two registries and causes drift.

## Skills Convention

`skills/*.md` are local project playbooks. They are not installed Codex skills. To use one, read the file and follow its procedure. If a reusable Codex skill is created later, it must point back to the same local playbook or replace it as the canonical source.
