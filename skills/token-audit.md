# Skill: Token Audit — Context Overhead Check

> **Purpose:** Find invisible token waste in CLAUDE.md, hooks, MCPs, plugins, skills, and session length
> **Used by:** User (orchestrator), Niels (docs-sync) when sessions feel bloated
> **Status:** Active
> **Created:** 2026-05-03
> **Last Improved:** 2026-05-03

## When to Use

Invoke this skill when:
- Hitting Claude usage limits more than once a week
- Sessions feel slow or quotas tighten unexpectedly
- After installing new plugins / MCPs / skills (audit the new floor)
- Monthly hygiene check — even if everything feels fine

## Input

- The project root directory (must contain `.claude/` and/or `CLAUDE.md`)
- Optional: read access to `~/.claude/` for global config

## Background

Every Claude Code turn pre-charges these tokens *before* your prompt is read:

1. CLAUDE.md (global + project) — always loaded
2. UserPromptSubmit hook injections — fire on every prompt
3. SessionStart hook output — fires once per session
4. MCP tool schemas — every connected server, every request
5. Conversation history — re-tokenized on every turn (grows linearly)
6. Cache misses on resume — 5-min default TTL; coffee break ≈ full price
7. Skill SKILL.md content — when relevance is detected (often over-eager)
8. Extended thinking — `<thinking>` blocks even on trivial questions
9. Wrong-direction generation — output tokens you let finish before correcting

Productive tokens are the residual. If your CLAUDE.md is 2,000+ words and you have 4 plugins with prompt hooks, productive share can drop below 30%.

## Procedure

### Step 1: Measure the Baseline

```bash
# CLAUDE.md size — target combined < 1,200 words (~1,500 tokens)
wc -w ~/.claude/CLAUDE.md 2>/dev/null
wc -w CLAUDE.md 2>/dev/null

# Active hooks — anything in UserPromptSubmit / SessionStart inflates every turn
jq '.hooks // {} | keys' ~/.claude/settings.json 2>/dev/null
jq '.hooks // {} | keys' .claude/settings.json 2>/dev/null

jq '.hooks.UserPromptSubmit // empty' ~/.claude/settings.json 2>/dev/null
jq '.hooks.UserPromptSubmit // empty' .claude/settings.json 2>/dev/null
jq '.hooks.SessionStart // empty' ~/.claude/settings.json 2>/dev/null
jq '.hooks.SessionStart // empty' .claude/settings.json 2>/dev/null

# Connected MCPs — each ships its tool schema on every request
jq '.mcpServers // {} | keys' ~/.claude/settings.json 2>/dev/null

# Installed skills/plugins — each loads when relevance is detected
ls ~/.claude/plugins/ 2>/dev/null
ls ~/.claude/skills/ 2>/dev/null
```

### Step 2: Apply the Targets

| Pattern | Target | Fix |
|---------|--------|-----|
| CLAUDE.md combined | < 1,200 words | Move tables to `agents/README.md`, `skills/README.md`, `docs/README.md`. Convert verbose rules into 3-word imperatives. Delete `[NOT YET CONFIGURED]` sections you'll never fill. |
| UserPromptSubmit hooks | ≤ 1 (e.g. git branch) | Disable any hook you can't justify per-prompt. |
| SessionStart hooks | ≤ 2 | Remove "loaded successfully" notifications. |
| Stop / PostToolUse stubs | Empty until configured | Don't ship placeholder echoes — they're noise tokens. |
| Always-on MCPs | 3 | Remove unused servers from `mcpServers`. Re-enable per-session when needed. |
| Active skills/plugins | 3–5 | Disable anything you haven't invoked in 7 days. |
| Conversation length | ≤ 20 messages | Use `/compact` (not `/clear`) when continuity matters. Edit the prior message instead of stacking follow-ups. |
| Cache TTL (paid plans) | 1 hour if 10+ resumes/session | Cache writes 2× base, reads 0.1× base. Pays for itself fast. |
| Extended thinking | Off by default | Toggle on per-message for architecture / hard debugging. |
| Wrong-direction output | Stop early | Cmd+. (mac) / Esc-Esc to checkpoint-rewind. |

### Step 3: Report Findings

Present a table with one row per pattern: current vs target, and the proposed fix. Wait for user confirmation before applying anything that changes settings or removes plugins.

### Step 4: Apply Approved Fixes

- CLAUDE.md edits — extract tables, condense rules, never delete project facts.
- `.claude/settings.json` — empty unused hook arrays; never delete the file.
- MCP / plugin removal — confirm with user first; document in `## Improvement Log`.

### Step 5: Update Documentation (MANDATORY)

- Note the before/after word count of CLAUDE.md in this skill's `## Improvement Log`
- If a recurring pattern emerges (e.g. "every bootstrap adds X tokens"), promote to a convention in CLAUDE.md
- Update `skills/README.md` cadence if you change how often this runs

## Output

- A short report: current sizes, target sizes, proposed fixes
- Applied fixes (with user approval)
- Updated `## Improvement Log` entry

## Project-Specific Notes

> Populated after bootstrap. Note the project's CLAUDE.md baseline word count so drift is measurable over time.

[NOT YET CONFIGURED]

## Quality Criteria

- [ ] Combined CLAUDE.md word count measured and recorded
- [ ] All UserPromptSubmit hooks justified or disabled
- [ ] No placeholder hook echoes shipping noise
- [ ] MCP list trimmed to actually-used servers
- [ ] Findings discussed with user before destructive changes
- [ ] Improvement log updated with before/after metrics

## Improvement Log

> After each use, record: date, context, what worked, what to improve.
> Format: `- [DATE] [CONTEXT]: [OBSERVATION] → [IMPROVEMENT]`

- 2026-05-03 INITIAL: Skill created based on 90-day token-instrumentation study showing 73% of tokens going to overhead (CLAUDE.md bloat 14%, history re-reads 13%, hook injection 11%, cache misses 10%, skill loading 7%, MCP schemas 6%, extended thinking 5%, wrong-direction output 4%, SessionStart hooks 3%). Baseline CLAUDE.md target: < 1,200 words combined.
