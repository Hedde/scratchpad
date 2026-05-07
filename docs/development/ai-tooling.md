# AI Tooling Adapters

> Keep tool-specific integration thin. Project policy lives in one shared blueprint.

## Source of Truth

| Layer | Path | Purpose |
|-------|------|---------|
| Project blueprint | `CLAUDE.md` | Canonical rules, lifecycle, quality framework, agent/skill catalog |
| Codex adapter | `AGENTS.md` | Codex entry point and runtime mapping |
| Claude adapter | `.claude/` | Claude Code rules, hooks, and native skill wrappers |
| Persona catalog | `agents/` | Cross-tool named specialists |
| Playbook catalog | `skills/` | Cross-tool workflow procedures |
| Prompt templates | `agent-briefs/` | Reusable prompts for recurring agent tasks |
| Durable knowledge | `docs/` | Architecture, workflow, testing, operations, UI, feature docs |

## Drift Rules

- **[MUST]** Put durable project rules in `CLAUDE.md` or `docs/`, not in tool adapters.
- **[MUST]** Keep `AGENTS.md` and `.claude/` as thin adapters.
- **[MUST]** Update `docs/development/ai-tooling.md` when adding a new AI runtime, plugin layer, or agent registry.
- **[MUST NOT]** duplicate the `agents/` persona catalog into `.agents/`, `.claude/agents/`, or any other tool-specific registry.
- **[MUST NOT]** copy full skill procedures into Codex or Claude wrappers. Link or point back to `skills/`.

## Codex Notes

Codex reads `AGENTS.md` for repository instructions. The local `agents/*.md` files are project personas, not registered Codex subagent types. When explicit user permission exists to delegate, map personas onto Codex runtime roles and include the relevant persona guidance in the subagent prompt.

Repo-root `.agents/` is reserved for Codex plugin marketplace metadata only. Create it only when plugins are actually present.

## Claude Notes

Claude Code uses `CLAUDE.md` as the trigger/orchestrator file. `.claude/rules/` and `.claude/settings.json` provide Claude-native path rules and hooks. Claude-native skills under `.claude/skills/` must either be tool-specific wrappers or clearly documented exceptions; generic procedures belong in `skills/`.
