# Brief: Docs Audit

**Agent:** `docs-sync` (Niels)
**Purpose:** Audit + fix-pass on a documentation section for stubs, dead references, frontmatter consistency, and redundancy.

## Parameters

- `{{SCOPE}}` — folder(s), e.g. `docs/features/` or `docs/architecture/ + docs/operations/`
- `{{EXCLUDE}}` — subfolders to skip (default: `docs/backlog/` if you use one)
- `{{FOCUS}}` — optional: specific focus, e.g. `stubs+dead-refs` or `frontmatter+redundancy`

## Brief template

```
Do a full audit + fix-pass on `{{SCOPE}}`. Work IN-PLACE: edit files, don't create new ones unless splitting or consolidating.

## Scope
- Touch ONLY files under `{{SCOPE}}`
- NOT `{{EXCLUDE}}`

## Concrete fixes

### 1. Clean up TODO-stubs
Grep for `<!-- TODO`, `### X (TODO)`, `TBD`. For each: either document current behavior (check the code in the implementation folder), or remove the placeholder.

### 2. Remove dead cross-references
Check all `[text](target.md)` links — verify the target exists. Remove or fix dead links. If removing a link leaves an empty section, remove the whole section.

### 3. Normalize frontmatter
All docs should have consistent YAML frontmatter with minimum `title` and `layer` (or equivalent project-specific keys). Add missing frontmatter. Strip outdated entries from `related:` lists.

### 4. Synchronize _index.md
Check `{{SCOPE}}/_index.md` — every file in the folder should be listed, alphabetical, with a short 1-line description.

### 5. Writing style + compaction
- Present-tense, concise
- If a doc is >30% "how it used to be" / "we replaced X with Y" — cut. Describe the present
- Clear overlap between files: resolve with cross-references instead of repetition. Short repetition for context is OK

### 6. Dead links (full sweep)
Check every internal link points to an existing file.

## Focus (if specified)
{{FOCUS}}

## Working style
- Quick grep/glob first to validate the full issue list
- Batch fixes — don't plan file by file
- Don't touch code, only markdown within scope
- Final report: 1-paragraph summary + list of changed files

No commit — the user handles that.
```

## Example fill

```
{{SCOPE}}   = docs/features/
{{EXCLUDE}} = docs/backlog/
{{FOCUS}}   = (empty — full audit)
```
