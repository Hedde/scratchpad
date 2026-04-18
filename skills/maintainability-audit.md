# Skill: Maintainability Audit

> **Purpose:** Measure the codebase against the SIG Maintainability Model (ISO/IEC 25010 derivative). Produces a star-rating per quality property and actionable recommendations.
> **Used by:** Mark (qa-lead), invoked periodically
> **Status:** Active
> **Created:** 2026-04-18
> **Last Improved:** 2026-04-18

## When to Use

- **Periodic** — every 2-4 weeks during active development, or after each milestone
- **On request** — "how's the code quality?" / "should we refactor?"
- **Before a major release** — catch accumulating debt before it bites
- **After a sprint with heavy code additions** — verify quality didn't degrade

**Not for:** per-PR reviews (use `code-review.md`). SIG audit is a macro-view of the whole system.

## Input

- Full codebase
- Prior audit report (if exists) — for trend comparison
- Test coverage data (coverage.xml, lcov, excoveralls.json, etc.)

## The SIG Maintainability Model — 9 system properties

Each property scores **★☆☆☆☆ to ★★★★★** based on percentile vs. industry benchmark. Not all languages have exact thresholds — use the closest equivalent and note which.

| Property | Measures | How |
|----------|----------|-----|
| **Volume** | Total size (man-month equivalent) | Lines of code (LoC) per file, project total |
| **Duplication** | Copy-pasted code | % of duplicated lines (6+ consecutive) |
| **Unit size** | Function/method length | % of units >60 LoC |
| **Unit complexity** | Cyclomatic complexity per function | % of units with McCabe >5 / >10 / >20 |
| **Unit interfacing** | Parameter count | % of units with >4 parameters |
| **Module coupling** | Incoming dependencies | % of modules with high fan-in (framework-mandated coupling is acceptable) |
| **Component balance** | Top-level components evenly sized | Deviation from equal distribution |
| **Component independence** | Cross-component calls | % of calls crossing component boundaries |
| **Test code ratio** | Test LoC / production LoC | Ratio, plus statement coverage % |

## Procedure

### Step 1: Check data freshness

Before measuring: verify that coverage / lint / metrics files are recent (<24h old). If stale, ask the user to regenerate.

### Step 2: Measure

Use the tools appropriate for the stack. Common examples:

| Language | Common tools |
|----------|-------------|
| Elixir | `mix credo`, `mix xref`, custom LOC scripts |
| Python | `radon`, `pylint`, `coverage.py`, `pydeps` |
| JS/TS | `complexity-report`, `eslint`, `jest --coverage`, `madge` |
| Go | `gocyclo`, `go vet`, `go-cover` |
| Rust | `clippy`, `cargo-count`, `cargo-tarpaulin` |
| Java | `PMD`, `JaCoCo`, `SpotBugs` |

For each of the 9 properties:
1. Measure with the chosen tool
2. Map to SIG bands (see thresholds below)
3. Note exact vs. estimated — be honest about measurement limits

### Step 3: Map to SIG bands

Rough mid-industry thresholds (SIG benchmark 2020, language-agnostic — adjust by ±20% per-language):

| Property | ★★★★★ (top 5%) | ★★★★☆ | ★★★☆☆ | ★★☆☆☆ | ★☆☆☆☆ |
|----------|--------------|--------|--------|--------|--------|
| **Unit size** (% >60 LoC) | <3% | <10% | <22% | <38% | ≥38% |
| **Unit complexity** (McCabe — sum of risk-weighted ratios) | ★ moderate <10%, high <5%, very-high <0.5% | | | | |
| **Unit interfacing** (% >4 params) | <4% | <10% | <19% | <32% | ≥32% |
| **Duplication** | <3% | <5% | <10% | <20% | ≥20% |
| **Module coupling** | <10% high fan-in | <20% | <40% | <70% | ≥70% |
| **Coverage** | >95% | >80% | >60% | >40% | ≤40% |

> **Never inflate.** <80% coverage is never 5 stars, even if "good for this framework."

### Step 4: Produce report

```
MAINTAINABILITY AUDIT — <project name> — <date>
═══════════════════════════════════════════════

Volume:                 <LoC> (≈ <man-months> at 10k LoC/mm)
Duplication:            ★★★★☆  (<percent>%)
Unit size:              ★★★☆☆  (<percent>% >60 LoC)
Unit complexity:        ★★★☆☆  (moderate <x>%, high <y>%, very-high <z>%)
Unit interfacing:       ★★★★☆  (<percent>% >4 params)
Module coupling:        ★★★☆☆  (<percent>% high fan-in)
Component balance:      ★★★★☆  (stddev <value>)
Component independence: ★★★☆☆  (<percent>% cross-component calls)
Test code ratio:        ★★★★☆  (ratio <x>, coverage <y>%)

Overall maintainability: ★★★★☆ (SIG 4-star — market median is 3-star)

Measurement notes:
  - <property>: exact | estimated (reason)
  - Comparable to industry median in <category>

Trend vs. previous audit (<date>):
  - ↑ <property>: <old> → <new>
  - ↓ <property>: <old> → <new>
  - = <property>: unchanged

Top 5 improvement candidates (highest ROI):
  1. <file or module>: <issue> → <concrete action>
  2. ...

Framework-inherent patterns (cannot reduce, do not penalize):
  - <pattern>: <why it's framework-mandated>

Next audit recommended: <date>
```

### Step 5: Apply insights

- Feed the top 5 improvements into the backlog or the next sprint.
- For any property that dropped ≥1 star since the last audit: spawn `performance-engineer` (Daan) or `feature`/`fix` to investigate.
- Promote stable high-scoring patterns to conventions.

## Rules

- **[MUST]** Measure all 9 properties — if one can't be measured exactly, estimate and say so
- **[MUST]** State measurement method per property (exact / estimated + reason)
- **[MUST]** Compare to SIG benchmarks, not only to prior audits — absolute position matters
- **[MUST NOT]** Inflate scores — <80% coverage is never 5-star
- **[MUST NOT]** Treat all coupling as bad — framework patterns (router ↔ handler, controller ↔ model) are normal
- **[SHOULD]** Distinguish intentional shortcuts (acceptable) from accidental mess (fix now)
- **[SHOULD]** Run on a schedule — `/loop 336h /maintainability-audit` (2-weekly) for active projects

## Output

- Star-rated report (see Step 4 template)
- Top 5 improvement candidates with concrete actions
- Trend analysis (if prior audit exists)
- Updated issues / backlog for top items

## Quality Criteria

- [ ] All 9 properties measured or clearly estimated
- [ ] SIG-benchmark comparison present (not only trend)
- [ ] Top 5 improvements are actionable, not vague
- [ ] Framework-inherent patterns separated from real debt
- [ ] Prior audit compared (if exists)

## Improvement Log

[No entries yet — this log grows with use]
