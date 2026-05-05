---
name: sig-audit
description: Realistische SIG/TÜViT-stijl maintainability audit. Geeft eerlijke scores, niet diplomatieke. Disqualificeert prototypes als "productie-grade" en weegt risico op codevolume, niet op unit-aantal.
---

# SIG Audit Skill — Realisme-eerst

Doel: een eerlijk SIG/TÜViT-stijl rapport produceren dat een echte auditor zou kunnen verdedigen. **Niet** een rapport dat zo gunstig mogelijk klinkt voor de eigenaar.

Als je merkt dat je iets gunstig formuleert "omdat het anders streng overkomt" — herschrijf het. SIG is streng. Je doel is calibratie, niet diplomatie.

---

## Project-Specific Configuration

> **[MUST]** Bootstrap (`skills/bootstrap-interview.md`) vult deze sectie. Zonder configuratie: ALEERST configureren, daarna pas auditen. Een audit zonder framework-context produceert verkeerde scores (zie anti-patroon "framework-context misbruiken").

### Stack
- **Hoofdtaal(en) + versie:** [NOT YET CONFIGURED]
- **Framework(s) + versie:** [NOT YET CONFIGURED]
- **Architectuur-stijl:** [NOT YET CONFIGURED] — bijv. monolith, modular monolith, microservices, serverless
- **Persistence:** [NOT YET CONFIGURED]
- **Test framework + coverage tool:** [NOT YET CONFIGURED]

### Meet-tooling per property
Welke concrete commando/tool meet welke property in dit project. `n.v.t.` als geen tool bestaat.

| Property | Tool / commando |
|----------|-----------------|
| Volume | [NOT YET CONFIGURED] |
| Duplication | [NOT YET CONFIGURED] |
| Unit Size | [NOT YET CONFIGURED] |
| Unit Complexity | [NOT YET CONFIGURED] |
| Unit Interfacing | [NOT YET CONFIGURED] |
| Module Coupling | [NOT YET CONFIGURED] |
| Component Balance | [NOT YET CONFIGURED] |
| Component Independence | [NOT YET CONFIGURED] |
| Component Entanglement | [NOT YET CONFIGURED] |
| Test Coverage | [NOT YET CONFIGURED] |

### Framework-mandated patterns
Lijst hier welke patronen door het gekozen framework worden afgedwongen — deze mogen vermeld worden bij scoring, maar niet als excuus om het overall-cijfer op te krikken.

[NOT YET CONFIGURED] — voorbeelden om te vervangen:
- *Phoenix LiveView*: callbacks `mount/3`, `handle_event/3`, `handle_params/3` zijn 3-param.
- *React*: hooks-volgorde regel; props-drilling op kleine schaal acceptabel.
- *Rails*: ActiveRecord callbacks koppelen schema en gedrag.
- *Spring*: dependency injection via annotaties veroorzaakt hoge fan-in op config-klassen.

### Kritieke paden
Modules / pakketten / endpoints waar een Very-High risk unit een **−1 ster cap** triggert. Bootstrap stelt deze vast op basis van domein.

[NOT YET CONFIGURED] — voorbeelden om te vervangen: auth-handler, payment processor, request-router, schema-migrations, sessie-store.

### Productie-readiness referenties
Per gate-item: waar in dit project bewijs te vinden is (of "ontbreekt").

| Gate | Bewijs / pad |
|------|--------------|
| CI met testruns | [NOT YET CONFIGURED] |
| Logging | [NOT YET CONFIGURED] |
| Error tracking | [NOT YET CONFIGURED] |
| Persistence | [NOT YET CONFIGURED] |
| Health-check endpoint | [NOT YET CONFIGURED] |
| Graceful shutdown | [NOT YET CONFIGURED] |
| Secrets management | [NOT YET CONFIGURED] |
| Deployment-config | [NOT YET CONFIGURED] |
| Onboarding-tijd documenteerd | [NOT YET CONFIGURED] |
| License + SBOM | [NOT YET CONFIGURED] |

### Project-specifieke afwijkingen op SIG-drempels
Alleen vullen na expliciete user-akkoord. Default: SIG-drempels gelden zoals gepubliceerd.

[NOT YET CONFIGURED]

---

---

## Pre-flight: classificeer het systeem (verplicht)

**Vóór** je metrics gaat verzamelen, classificeer het systeem. Dit bepaalt de meetlat.

| Klasse | Kenmerken | Meetlat |
|--------|-----------|---------|
| **Prototype / demo / vibe-code** | Geen tests, geen CI, geen persistence, < 1 dag werk, één developer, lokale demo | Niet certificeerbaar. Geef SIG-score "n.v.t. — prototype". Beschrijf wat er moet gebeuren om überhaupt te scoren. |
| **Intern tool / hobbyproject** | Wel iets van tests of structuur, maar niet productie-kritisch | Score eerlijk, maar kader: "intern, geen externe afhankelijkheden". |
| **Productie-grade** | Externe gebruikers, SLA-relevant, persistence, observability, CI/CD aanwezig | Volledige SIG-meetlat. Geen voordeel-van-de-twijfel. |

**Als de gebruiker vraagt "is dit productie-grade?":** wees een auditor, geen consultant. Een systeem zonder tests, zonder logging, zonder persistence, zonder CI is **geen** productie-grade — ongeacht of het draait.

### Productie-grade gate (alle moeten ✓ zijn)

Vóór je überhaupt sterren toekent als productie-systeem:

- [ ] Geautomatiseerde tests bestaan en draaien in CI
- [ ] Logging naar gestructureerd doel (geen `console.log` als enige output)
- [ ] Foutafhandeling met zichtbaarheid (error tracking / metrics)
- [ ] Persistence-strategie (state overleeft restart)
- [ ] Health-check / readiness endpoint
- [ ] Graceful shutdown
- [ ] Secrets buiten code
- [ ] Deployment-config gereproduceerbaar (Docker / IaC / scripts)
- [ ] README waarmee een nieuwe developer < 1 uur draaiend is
- [ ] Dependency- en license-manifest compleet

**Eén ✗ = "niet productie-grade".** Rapporteer dit als kop boven de scores. Geen verzachting.

---

## Harde caps (overschrijven percentielscores)

SIG's eindscore is geen gemiddelde, maar bepaalde tekortkomingen **cappen** het totaal. Pas deze caps toe vóór percentiel-vergelijking:

| Conditie | Cap op overall maintainability |
|----------|-------------------------------|
| Test code ratio = 0% (geen tests) | **★1** |
| Test code ratio < 25% | **★2** |
| Test coverage < 40% (waar meetbaar) | **★2** |
| Een Very-High risk unit op een kritiek pad (auth, payments, request-routing) | **−1 ster** op overall |
| > 25% van code-volume zit in Very-High risk units | **★2** |
| Productie-grade gate faalt | **n.v.t.** — geen sterren toekennen, alleen kwalitatief rapport |

**Reden voor caps:** SIG benchmarkt tegen 20.000+ systemen die tests, persistence en observability hebben. Een systeem zonder die basis is geen 35e-percentiel — het is buiten de verdeling.

---

## Anti-patronen bij scoring (niet doen)

**1. Afwezigheid belonen**
- ❌ "Geen modules → geen koppeling → ★5 component independence"
- ✅ "Geen modulestructuur — niet evalueerbaar (n.v.t.). Rode vlag voor uitbreidbaarheid."

- ❌ "Klein volume → ★5 volume score"
- ✅ "Klein volume — score irrelevant. SIG normaliseert op person-months; <100 PM zegt niets over kwaliteit."

- ❌ "Geen externe dependencies → ★5 supply chain"
- ✅ "Geen dependencies — supply chain attack surface laag. Zegt niets over interne kwaliteit."

**2. Unit-aantal in plaats van code-volume tellen**
- SIG weegt risk profile op **percentage van totaal codevolume**, niet aantal units.
- Eén `handleRequest` van 91 LOC met CC=43 in een 600-LOC bestand = ~15% van het volume in Very-High risk. Dat is **niet** "1 op 27 functies = 3.7%".
- Wees expliciet in de rapportage: "X% van codevolume zit in High/Very-High risk".

**3. Framework-context gebruiken om alles weg te verklaren**
- Phoenix LiveView callbacks ZIJN inherent 3-param. Vermeld het, maar gebruik het niet om elk parameter-issue weg te masseren.
- Onderscheid: "framework-mandated" (geef context) vs "eigen keuze" (gewoon scoren).
- Als 50% van de code framework-mandated patterns volgt, mag dat geen excuus worden voor overall ★4.

**4. "Goed voor [framework/taal/domein]"**
- ❌ "70% coverage is goed voor een Phoenix-app → ★5"
- ❌ "Voor een spel is dit acceptabel"
- ✅ "70% coverage = ★3 op SIG-percentielen. SIG vergelijkt over alle industrieën, niet binnen niche."

**5. Estimaten als veilige middelmaat scoren**
- ❌ "Duplication niet meetbaar → ★3 (gemiddeld)"
- ✅ "Duplication niet meetbaar → score onthouden, vermeld als limitatie. Geen sterren cadeau."

**6. Diplomatiek vocabulair**
- ❌ "ruimte voor verbetering", "kan worden geoptimaliseerd", "in lijn met goede praktijken"
- ✅ "voldoet niet aan 4★-drempel", "weegt zwaar op overall", "disqualificeert certificering"

---

## Calibratie-ankers

Lees deze hardop voor je een score toekent. Vergelijk je systeem met de ankers, niet met je gevoel.

### Test Code Ratio / Coverage
- **★5**: ≥80% lijn-coverage, mutation-testing of property-based tests, integration + unit + e2e
- **★4**: 60–80% coverage, integration tests, CI-blocking
- **★3**: 40–60% coverage, vooral happy paths
- **★2**: 20–40% coverage, alleen unit, niet CI-blocking
- **★1**: < 20% coverage, of geen tests
- **n.v.t.**: 0 tests = niet certificeerbaar als productie

### Unit Complexity (op codevolume gewogen)
- **★5**: 0% volume in Very-High; > 90% in Low
- **★4**: < 5% volume in Very-High; > 75% in Low (SIG 4★-drempel)
- **★3**: 5–15% volume in Very-High
- **★2**: 15–30% volume in Very-High
- **★1**: > 30% volume in Very-High, of een kritiek-pad-unit met CC > 25

### Module/Component Architecture
- **★5**: duidelijke laagscheiding, expliciete public API per module, geen cross-laag-cycles
- **★4**: laagscheiding aanwezig, enkele framework-inherent cycles
- **★3**: enige modulariteit, maar lekkage tussen lagen
- **★2**: 2–3 monolithische bestanden zonder echte module-grenzen
- **★1**: alles in één bestand
- **n.v.t.**: te klein om architectuur te hebben — beschrijf, ken geen ster toe

---

## Verplichte rapport-secties

Elk audit-rapport bevat (in deze volgorde):

### 1. Classificatie
"Dit systeem is **[prototype / intern tool / productie-grade]**." Met onderbouwing op basis van de gate.

### 2. Disqualifiers (indien van toepassing)
Lijst alle gate-faals expliciet op. Geen impliciete weglating.

### 3. Scope-disclaimer
- Welke metrics zijn exact meetbaar?
- Welke geschat? (en met welke ondergrens van betrouwbaarheid)
- Welke n.v.t.?

### 4. Scores per property
Tabel met:
- Meting (cijfer/percentage)
- Drempel
- Ster
- **Eén regel waarom** — geen marketing, alleen feit

### 5. Operationele gaps (productie-readiness)
Aparte tabel los van source-metrics:
- Logging, monitoring, alerting
- Persistence, backup, recovery
- CI/CD, deployment
- Secrets, config-management
- Documentation, runbook
- License, SBOM, dependency-policy

### 6. Top-3 disqualifiers met ROI
Niet "verbeterpunten". **Disqualifiers**: wat moet veranderen voor het volgende sterren-niveau.

### 7. Eerlijke conclusie
- Eén zin: "Dit systeem scoort **[ster]** op SIG-maintainability."
- Eén zin: "Het is [wel/niet] productie-grade."
- Geen optimistische slotparagraaf. Auditor sluit met feit, niet met aanmoediging.

---

## Realisme-checklist (uitvoeren vóór indienen)

Lees je conceptrapport en check eerlijk:

- [ ] Heb ik ergens een ★ toegekend aan **de afwezigheid van iets**? (refactor)
- [ ] Heb ik unit-aantal gerapporteerd waar SIG codevolume verwacht? (herbereken)
- [ ] Staat er ergens "goed voor [niche]" als rechtvaardiging? (verwijder)
- [ ] Klopt de overall-ster met de harde caps?
- [ ] Heb ik de productie-gate expliciet beoordeeld?
- [ ] Zou ik dit rapport durven verdedigen tegenover een SIG-auditor die kritisch tegenvraagt?
- [ ] Is de conclusie eerlijk, of geruststellend?

Als je twijfelt tussen twee sterren: **kies de lagere**. SIG's kalibratie is bewust streng (50% van systemen zit onder ★3).

---

## Wat NIET het werk is van deze skill

- **Niet:** een coachende roadmap schrijven. Audit rapporteert toestand, niet verbeterplan.
- **Niet:** kwaliteit verkopen aan stakeholders. Geef cijfers, geen narratief.
- **Niet:** framework- of taalspecifieke uitzonderingen verzinnen om scores op te krikken.
- **Niet:** "voortgang sinds vorige audit" rapporteren. Alleen huidige toestand vs SIG-drempels.

---

## SIG-model essentials (referentie)

### 9 source-properties (mapped op ISO 25010)

| # | Property | Meet | 4★-drempel |
|---|----------|------|-----------|
| 1 | Volume | Totale omvang (LOC of person-months) | 100–500K LOC = medium |
| 2 | Duplication | % gedupliceerde code | < 5% |
| 3 | Unit Size | LOC per functie/methode | > 15 LOC: max 47.1% van volume; > 30: max 23.1%; > 60: max 8.3% |
| 4 | Unit Complexity | Cyclomatic complexity per unit | ≥ 75% van units met CC ≤ 5 |
| 5 | Unit Interfacing | Aantal parameters per unit | ≥ 3 params: max 15.0%; ≥ 5: max 3.3%; ≥ 7: max 0.9% |
| 6 | Module Coupling | Inkomende afhankelijkheden | > 20 deps: max 5.6%; > 50: max 1.9% |
| 7 | Component Balance | Gelijke verdeling code over componenten | Even verdeling |
| 8 | Component Independence | % code in verborgen modules | ≥ 93.7% verborgen |
| 9 | Component Entanglement | Anti-patronen tussen componenten | Geen cycles, geen layer-bypass |

### Risk-bins (taal-onafhankelijk)

| Property | Low | Moderate | High | Very High |
|----------|-----|----------|------|-----------|
| Unit Size (LOC) | 1–15 | 16–30 | 31–60 | > 60 |
| Unit Complexity (CC) | 1–5 | 6–10 | 11–25 | > 25 |
| Unit Interfacing (params) | 0–2 | 3–4 | 5–6 | ≥ 7 |

### Sterren-distributie (5%-30%-30%-30%-5%)

- ★5 = top 5% van industrie
- ★4 = 5e–35e percentiel (boven gemiddeld)
- ★3 = 35e–65e percentiel (markt-gemiddeld)
- ★2 = 65e–95e percentiel (onder gemiddeld)
- ★1 = bottom 5% (kritisch risico)

44% van alle systemen zit onder SIG's aanbevolen rating. ★3.5 is al "boven gemiddeld". Wees streng — de meeste software is middelmaat.

---

## Workflow

1. **Classificeer** systeem (prototype / intern / productie). Loop de productie-gate door.
2. **Verzamel metrics** — zoveel mogelijk exact, anders eerlijk geschat met betrouwbaarheidslabel.
3. **Pas harde caps toe** voordat je percentielen vergelijkt.
4. **Score** elke property met de calibratie-ankers, niet op gevoel.
5. **Schrijf rapport** in vereiste structuur.
6. **Run de realisme-checklist** vóór indienen.
7. **Lever conclusie eerlijk** — geen geruststelling, geen verkooppraat.

---

## Slot

Een goede audit doet pijn aan de eigenaar als de software dat verdient. Als je rapport iedereen tevreden stelt, heb je je werk niet gedaan.
