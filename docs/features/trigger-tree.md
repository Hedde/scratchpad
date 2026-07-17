# Feature: trigger-tree

> **Status:** Complete (plugin v0.1.0)
> **Created:** 2026-07-17

## Purpose

Observability-laag over de documentatie-router, verpakt als Claude Code plugin (`tt`).
Elke read van een documentatiebestand (docs/, agents/, skills/, agent-briefs/,
CLAUDE.md, AGENTS.md, .claude/rules|skills) wordt shell-side gelogd via plugin-hooks —
nul model-tokens. De telemetrie beantwoordt: welke docs worden bij welke taken
daadwerkelijk geraadpleegd, welke paden zijn dood, en waar zoekt het model in plaats
van gerouteerd te worden?

Bewuste designkeuze: de discovery zelf blijft model-driven (CLAUDE.md → docs/README.md
→ index-instructies). trigger-tree **meet** die discovery deterministisch en scherpt de
router datagedreven aan — het is géén tweede routeringsmechanisme.

## User Flow

Alles via één commando (root-skill van de plugin, strikte outputdiscipline — alleen
resultaat, geen tussenstappen):

1. Sessies draaien normaal; plugin-hooks loggen onzichtbaar naar `.trigger-tree/history.jsonl`.
2. Statusline (project-setting, want plugins kunnen geen statusline leveren) toont live
   `🌳 3 files · 3 folders · depth 2 ● docs/ui/patterns.md` — dot pulst op leeftijd van
   de laatste read (● groen <90s, ◐ amber <10min, ○ dim ouder).
3. `/tt status` — compact snapshot in de chat.
4. `/tt watch [demo|replay]` — opent het live ASCII pulse-dashboard in een nieuw
   Terminal-venster (heat-tree; reads flitsen wit en rippelen omhoog door parent-folders).
5. `/tt insights` — kort rapport in de chat (dode paden in 3 categorieën, hunting,
   max 3 routervoorstellen) + link naar een volledig HTML-rapport (Artifact of
   `.trigger-tree/report.html`).
6. `/tt help` — commando-overzicht.

## Technical Design

### Plugin (externe repo: [github.com/Hedde/trigger_tree](https://github.com/Hedde/trigger_tree))

De plugin leeft sinds 2026-07-17 in een eigen publieke repo (Engelstalig, MIT). Dit
project is consumer: `extraKnownMarketplaces` + `enabledPlugins` in
`.claude/settings.json` zorgen dat teamgenoten een installatie-prompt krijgen.
Terminologie volgt een maturity-model: 0 reads = *untouched*; pas bij een volwassen
meetperiode (`mature`: ≥100 reads, ≥7 dagen, ≥3 sessies) heten die *dead-path
candidates*.

Layout van de plugin-repo:

| Onderdeel | Responsibility |
|-----------|---------------|
| `.claude-plugin/plugin.json` | Manifest; plugin heet `tt` |
| `SKILL.md` (plugin-root) | Root-skill → kaal `/tt`-commando met subcommand-dispatch |
| `hooks/hooks.json` | SessionStart / UserPromptSubmit / PostToolUse(Read\|Glob\|Grep) → `tt-log.sh` |
| `scripts/tt-config.sh` | Default-config (watch/scan/always-loaded regexes) |
| `scripts/tt-log.sh` | Logger; filtert non-doc paden, append JSONL |
| `scripts/tt-stats.py` | Deterministische aggregator → stats-JSON |
| `scripts/tt-report.py` | Stats → self-contained HTML-rapport |
| `scripts/tt-watch.py` | Live terminal-dashboard (tail, `--demo`, `--replay`) |
| `scripts/tt-open.sh` | Opent tt-watch in nieuw Terminal-venster (osascript) |
| `scripts/tt-statusline.sh` | Statusline-script (kopie; registratie blijft project-setting) |

De plugin-repo is zijn eigen marketplace (`/plugin marketplace add Hedde/trigger_tree`
→ `/plugin install trigger-tree@trigger-tree`; het commando blijft `/tt`); lokaal testen kan met
`claude --plugin-dir ../trigger_tree`. Per-project override van de config:
`.trigger-tree/config.sh` (gecommit; de rest van `.trigger-tree/` is gitignored).

### Event log (`.trigger-tree/history.jsonl`)

| Event | Velden | Bron |
|-------|--------|------|
| `session` | ts, session | SessionStart hook |
| `prompt` | ts, session, prompt (eerste 200 chars) | UserPromptSubmit hook |
| `read` | ts, session, tool, path (relatief), agent | PostToolUse op Read |
| `scan` | idem — Glob/Grep in docs-mappen = "hunting" | PostToolUse op Glob\|Grep |

Fingerprint = sha1 (10 hex) van de gesorteerde set doc-paden gelezen tussen twee
prompt-markers binnen één sessie; identieke sets over sessies heen gegroepeerd →
taaktype-patronen.

## Edge Cases

- **Altijd-geladen context is onzichtbaar voor de telemetrie**: CLAUDE.md en
  `.claude/rules` worden in de system prompt geïnjecteerd, SKILL.md's laden via de
  Skill-tool — geen Read-tool-call, dus geen event. Daarom sluit `TT_ALWAYS_LOADED_REGEX`
  ze uit van dead-path-detectie (`always_loaded` in de stats). "0 docs consulted" bij
  sessiestart is dus correct: de router is geladen, discovery is nog niet gebeurd.
- Non-doc reads: gefilterd in de hook zelf (exit 0), geen log-regel.
- Subagent-reads: gelogd met `agent_type`; een alleen-door-subagents-gelezen file is niet dood.
- Torn writes in de JSONL: aggregator slaat onparseerbare regels over.
- Glob/Grep zonder `path` (cwd-default): genegeerd (MVP).
- Nieuwe files lijken "dood": `/tt insights` weegt `observed_from` mee.

## Technical Decisions

### Decision: meten, niet forceren

- **Options considered:** (A) deterministische context-injectie per prompt via
  UserPromptSubmit, (B) model-driven discovery + deterministische telemetrie.
- **Chosen:** B.
- **Rationale:** A kost elke prompt tokens en vecht met de bestaande router; B is gratis
  (shell-side) en maakt de router aantoonbaar beter. A blijft mogelijk als latere fase
  (history-gedreven hints injecteren), gebouwd óp de data van B.

### Decision: kaal `/tt` via root-skill met subcommands

- **Options considered:** meerdere plugin-skills (`/tt:watch`, `/tt:insights`, …) of
  één root-SKILL.md met subcommand-dispatch (`/tt watch`, `/tt insights`).
- **Chosen:** root-skill. Een plugin zonder `skills/`-map maar mét root-SKILL.md krijgt
  het kale commando; meerdere skills worden altijd genamespaced.
- **Rationale:** `/tt <sub>` leest als één tool (vgl. git); de dispatch-instructies
  bevatten meteen de outputdiscipline (stil werken, alleen resultaat).

### Decision: statusline blijft project-setting

- **Rationale:** plugin-`settings.json` ondersteunt alleen `agent` en
  `subagentStatusLine`. Het script ship met de plugin; registratie gebeurt per project
  (hier: `.claude/settings.json` → `scripts/tt-statusline.sh`, `refreshInterval: 5`).

## Open Questions

- [ ] Skill-tool-invocaties loggen (PostToolUse matcher `Skill`) zodat ook
      SKILL.md-gebruik meetbaar wordt in plaats van `always_loaded`.
- [ ] Codex-adapter: Codex heeft geen hook-systeem; kan een wrapper in dezelfde
      history.jsonl bijschrijven?
- [ ] Drempelwaarden voor "dood" (nu: 0 reads over hele meetperiode) — kalibreren na
      eerste echte `/tt insights`-run.
- [ ] Marketplace naar GitHub + `extraKnownMarketplaces`/`enabledPlugins` in
      `.claude/settings.json` zodat teamgenoten een installatie-prompt krijgen.

## Testing Notes

- Hook-logger: gesimuleerde stdin-JSON events in geïsoleerde scratch-dir (filtering,
  scan-detectie, subagent-attributie).
- Statusline: verse read → ● groen, oudere → ◐ amber, geverifieerd op ANSI-codes.
- Dashboard: `--demo --seconds N` en `--replay` headless gedraaid; pulse-decay en
  folder-ripple zichtbaar in opeenvolgende frames; exit 0.
- Aggregator + report: gedraaid tegen echte history; `always_loaded` correct gescheiden
  van `dead_paths`; `claude plugin validate` → passed.
