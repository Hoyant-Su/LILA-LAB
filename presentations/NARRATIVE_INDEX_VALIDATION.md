# Validating Narrative Indices Across Domains
## A General Framework for Cross-Domain Narrative Index Validation

> **Core insight:** Validation is about **triangulation** — no single test proves an index is "correct." You need converging evidence from multiple sources. The framework generalizes; only the specific indicators change.

---

## 1. The Validation Hierarchy

Every domain follows the same validation logic, just with different external data:

| Level | Validity Type | Question | Economics Example |
|-------|---------------|---------|-------------------|
| 1 | **Face Validity** | Do the narratives make sense to domain experts? | "Do economists agree the index captures economic discourse?" |
| 2 | **Content Validity** | Does the annotation schema capture the construct? | "Do the 12 economic schema fields cover all relevant economic concepts?" |
| 3 | **Inter-Annotator** | Do independent annotators agree? | "Cohen's κ > 0.70 between Claude and GPT-4o" |
| 4 | **Concurrent Validity** | Does the index correlate with current outcomes? | "Index vs CPI: r = −0.75" |
| 5 | **Predictive Validity** | Does the index predict future outcomes? | "VAR beats random walk by 20.9% at 6 months" |
| 6 | **Construct Validity** | Convergent + discriminant tests | "Economic index correlates with econ data, NOT with weather data" |
| 7 | **Causal Validity** | Does narrative Granger-cause or respond to shocks? | "CPI Granger-causes narratives (p = 0.01)" |
| 8 | **Replication** | Can others reproduce it? | "Independent team reproduces the index ±5%" |

### The Default Chain

Most domains cannot achieve all 8 levels immediately. The pragmatic path:

```
Step 1: Face + Content validity     (schema design with domain experts)
Step 2: Inter-annotator reliability  (κ > 0.70 on a test set)
Step 3: Event studies                (known shocks → expected index movement)
Step 4: Source consistency           (multiple outlets tell the same story)
Step 5: Construct validity           (your index ≠ other indices)
Step 6: Concurrent/Predictive        (if external data exists)
```

---

## 2. Domain-by-Domain Validation

### 2.1 Health Domain — "Health Narrative Index"

| Validation Type | What You Measure Against | Data Source | Example Hypothesis |
|----------------|------------------------|-------------|-------------------|
| **Concurrent** | Disease prevalence, hospitalization rates | WHO, ministries of health, CDC | "Does a 'disease X fear' narrative correlate with actual hospital admissions for X?" |
| **Concurrent** | Vaccination rates, treatment adoption | National health surveys | "Does anti-vaccine narrative prevalence correlate with lower vaccination uptake?" |
| **Concurrent** | Healthcare utilization (clinic visits, ER visits) | Insurance claims, hospital records | "Do health anxiety narratives predict ER visit spikes?" |
| **Predictive** | Future disease outbreaks | Epidemic surveillance systems | "Does a dengue narrative index predict confirmed cases 2 months ahead?" |
| **Predictive** | Policy response speed | Government gazettes, policy announcements | "Do health crisis narratives precede policy action?" |
| **Event-based** | Known health shocks (pandemic waves, drug shortages) | Known event timelines | "Did the narrative index spike during COVID waves?" |
| **Construct** | Compare different diseases (known severity) | Baseline epidemiology | "Does a high-mortality disease get more narrative coverage than a low-mortality one?" |

**Example hypothesis:** A "vaccine hesitancy narrative index" extracted from Hindi news → validated against district-level vaccination rates (r = −0.6, p < 0.01) → Granger-causes vaccination decline at 2-month lag.

---

### 2.2 Climate / Environment Domain — "Climate Narrative Index"

| Validation Type | What You Measure Against | Data Source | Example Hypothesis |
|----------------|------------------------|-------------|-------------------|
| **Concurrent** | Extreme weather event frequency | NOAA, national meteorological agencies | "Does climate narrative intensity spike during heatwave/flood seasons?" |
| **Concurrent** | Carbon emissions, temperature anomalies | NASA, IPCC data | "Do 'climate crisis' narratives correlate with actual warming trends?" |
| **Concurrent** | Air/water quality indices | Environmental monitoring stations | "Do pollution narratives correlate with measured AQI?" |
| **Predictive** | Policy adoption timelines | UNFCCC submissions, national climate plans | "Do climate urgency narratives precede carbon pricing adoption?" |
| **Predictive** | Renewable energy investment | BloombergNEF, IEA | "Do green energy narratives predict investment flows?" |
| **Event-based** | Known disasters (cyclones, floods, wildfires) | EM-DAT disaster database | "Did the narrative index correctly spike during known events?" |
| **Cross-domain** | Economic indicators | GDP, insurance payouts | "Do climate narratives predict economic losses from disasters?" |

**Example hypothesis:** A "climate urgency narrative index" from Swahili news → validated against Kenyan drought frequency data (r = 0.55) → peaks 2 months before emergency declarations.

---

### 2.3 Education Domain — "Education Narrative Index"

| Validation Type | What You Measure Against | Data Source | Example Hypothesis |
|----------------|------------------------|-------------|-------------------|
| **Concurrent** | Literacy rates, enrollment rates | UNESCO, national education ministries | "Do 'education crisis' narratives correlate with declining enrollment?" |
| **Concurrent** | Education budget allocation | Government budget documents | "Do education funding narratives correlate with actual budget changes?" |
| **Concurrent** | Test scores, learning outcomes | PISA, national assessments | "Do 'quality of education' narratives correlate with test score trends?" |
| **Predictive** | Future enrollment, dropout rates | Education management information systems | "Do negative education narratives predict dropout increases next year?" |
| **Event-based** | Policy reforms, teacher strikes | Known event timelines | "Did the 'education reform' narrative spike before/after a major policy announcement?" |
| **Construct** | Compare different education levels | Baseline data | "Does primary education get more narrative attention than higher education, matching its larger enrollment?" |

---

### 2.4 Governance / Political Domain — "Governance Narrative Index"

| Validation Type | What You Measure Against | Data Source | Example Hypothesis |
|----------------|------------------------|-------------|-------------------|
| **Concurrent** | Approval ratings, trust indices | Gallup, Pew, national surveys | "Do anti-governance narratives correlate with falling approval ratings?" |
| **Concurrent** | Corruption perception indices | Transparency International | "Do corruption narratives correlate with CPI scores?" |
| **Predictive** | Election outcomes | Election commission data | "Do pre-election narratives predict voting patterns?" |
| **Predictive** | Policy stability, reform adoption | World Bank governance indicators | "Do governance crisis narratives predict policy reversals?" |
| **Event-based** | Known events (scandals, protests, elections) | Global Database of Events | "Did the narrative index spike during known corruption scandals?" |

---

### 2.5 Social / Inequality Domain — "Social Justice Narrative Index"

| Validation Type | What You Measure Against | Data Source | Example Hypothesis |
|----------------|------------------------|-------------|-------------------|
| **Concurrent** | Inequality metrics (Gini coefficient) | World Bank, national statistics | "Do inequality narratives correlate with measured inequality?" |
| **Concurrent** | Social unrest, protest events | ACLED, protest databases | "Do 'social justice' narratives precede protest events?" |
| **Concurrent** | Policy changes (minimum wage, social spending) | ILO, government data | "Do labor rights narratives correlate with minimum wage policy changes?" |
| **Predictive** | Future inequality measures | Lagged economic data | "Do rising inequality narratives predict widening Gini 2 years later?" |

---

### 2.6 Technology / Digital Domain — "Tech Narrative Index"

| Validation Type | What You Measure Against | Data Source | Example Hypothesis |
|----------------|------------------------|-------------|-------------------|
| **Concurrent** | Internet penetration, mobile adoption | ITU, GSMA | "Do 'digital transformation' narratives correlate with adoption rates?" |
| **Concurrent** | Venture capital investment, startup funding | Crunchbase, PitchBook | "Do 'AI boom' narratives precede funding increases?" |
| **Predictive** | Regulatory action (data privacy, AI regulation) | Government gazettes | "Do 'tech regulation' narratives predict policy action 6 months later?" |
| **Event-based** | Product launches, data breaches, regulatory fines | Known event timelines | "Did the 'privacy concern' narrative spike after major data breaches?" |

---

## 3. The General Validation Toolkit

These validation instruments work across **every domain**.

### 3.1 Event Studies (the most universally applicable)

Identify **known shock events** and test whether your narrative index responds correctly:

| Domain | Known Shock Event | Expected Index Movement |
|--------|-------------------|------------------------|
| Economics | Central bank rate hike | "Monetary policy" narrative spikes |
| Health | WHO declares pandemic | "Health crisis" narrative spikes |
| Climate | Major cyclone makes landfall | "Climate disaster" narrative spikes |
| Education | Teacher strike in capital | "Education crisis" narrative spikes |
| Politics | Major corruption scandal | "Governance failure" narrative spikes |
| Social | Landmark court ruling on rights | "Social justice" narrative spikes |
| Technology | Major data breach | "Privacy concern" narrative spikes |

**Method:**

```
1. Compile 10–20 known shock events with precise dates
2. For each event, compute the index value in:
   - 3 months before event (baseline)
   - Month of event
   - 3 months after event
3. Test: Is the event-month value significantly different from baseline?
   (t-test or Wilcoxon signed-rank)

   If 12/15 events show expected direction → strong validation (binomial test p < 0.02)
   If 8/15 events show expected direction → weak validation (need more work)
```

**Why event studies are the universal validator:** They require **no external time-series data** — only a list of dates and an expected direction. Every domain has known events.

---

### 3.2 Temporal Consistency Checks

```
Test:   Does the narrative index show smooth evolution or jump erratically?
Method: Month-to-month autocorrelation > 0.5
Logic:  Narratives don't change overnight. Large month-to-month swings indicate noise.
Domain: Universal — applies everywhere

Rule of thumb:
  autocorrelation > 0.7  → good temporal stability
  autocorrelation 0.4–0.7 → acceptable, investigate drivers of change
  autocorrelation < 0.4  → noisy index, need better measurement
```

---

### 3.3 Source Diversity Checks

```
Test:   Do different news sources tell the same story?
Method: Split by source (left-leaning vs right-leaning, broadsheet vs tabloid)
        Calculate separate indices. Measure pairwise correlations.

Expected:
  r > 0.7 between broadsheets → good (they agree on what's being discussed)
  r > 0.5 between broadsheet and tabloid → acceptable (different editorial priorities)
  r < 0.3 between sources → measurement problem (sources disagree on reality)

Domain: Universal — requires only 2+ news sources
```

**What divergent sources tell you:**
- If sources diverge systematically → you may be measuring **partisan framing**, not shared narratives
- If sources converge → the narrative is real enough to be picked up across editorial lines
- If sources diverge temporarily during elections → healthy democratic variation
- If sources always diverge → your index might be capturing noise

---

### 3.4 Survey Validation (gold standard where available)

```
Household surveys ask: "Do you think the economy/health/climate is getting 
better or worse?" (Consumer Confidence Index, perceived health risk, etc.)

Method:
  1. Align survey dates with index months
  2. Cross-correlate: narrative index(t) vs survey(t ± k months)
  3. If narrative leads survey by 1–3 months → narratives drive perception ✓
  4. If survey leads narrative → perception drives media coverage (also valid)

Domain: Universal — if survey data exists in your language/region.
```

**Survey sources by region:**

| Region | Available Surveys | Provider |
|--------|------------------|----------|
| South Asia | Gallup, Pew, national labor force surveys | Gallup, Pew Research |
| Africa | Afrobarometer, Gallup | Afrobarometer.org |
| Southeast Asia | Gallup, national surveys | Gallup |
| Latin America | LAPOP, Latinobarómetro | Vanderbilt, Latinobarómetro |
| Global | World Values Survey, Gallup World Poll | WVS, Gallup |

---

### 3.5 Expert Elicitation (when no external data exists)

```
When: No quantitative validation data is available for your domain or language.
How:
  1. Recruit 5–10 domain experts in your target language
  2. Ask them: "What were the top 5 narratives in [domain] during [year]?"
  3. Rank their responses (1st mention = 5 pts, 2nd = 4 pts, etc.)
  4. Compare expert rankings to your index's top narratives
  5. Compute Spearman rank correlation between expert and index rankings

Benchmark:
  ρ > 0.7 → good alignment between automated index and expert perception
  ρ < 0.5 → revisit your schema or annotation protocol

Domain: Universal, but most useful for novel domains.
```

---

### 3.6 Convergent-Discriminant Matrix

Test that your index measures what it claims to measure AND doesn't measure something else:

```
                    Health Index   Climate Index   Economic Index   Sports Index
Health Index            1.00           0.12            0.08            0.02
Climate Index           0.12           1.00            0.21            0.01
Economic Index          0.08           0.21            1.00            0.03
Sports Index            0.02           0.01            0.03            1.00

Expected pattern:
  ✓ Health and Economic indices → weakly correlated (different constructs)
  ✓ Climate and Economic → moderate correlation (climate affects economy — expected)
  ✓ Sports index → near-zero correlation with all (completely different domain)
  ✓ All diagonal values = 1.00 (trivially)
  ✓ All off-diagonal values < 0.5 (each index is measuring something distinct)

Failure modes:
  • If all indices correlate r > 0.5 → you've built a single "bad news" index
  • If theoretically related indices show r < 0.05 → possible construct under-coverage
```

---

### 3.7 LAG Structure Analysis (most nuanced)

Different domains have different **narrative-to-outcome lag structures**:

```
Domain       Narrative → Outcome Lag     Reason
────────     ───────────────────────     ──────────────────────
Economics    2–6 months                  Policy transmission, consumer behavior inertia
Health       1–3 months                  Disease progression + reporting lags
Climate      Weeks to years              Immediate (weather) vs delayed (policy)
Education    6–18 months                 School year cycles, policy implementation
Governance   3–12 months                 Budget cycles, electoral periods
Social       3–6 months                  Social movement mobilization
Technology   1–3 months                  Rapid news → investment cycles
```

**How to determine the correct lag:**
1. Compute cross-correlation function (CCF) between narrative index and outcome data
2. Identify the lag with maximum absolute correlation
3. If the peak is at negative lag (narrative leads outcome) → predictive validity ✓
4. If the peak is at positive lag (outcome leads narrative) → reactive measure (still valid but different interpretation)

---

## 4. The Easiest Path for Any New Domain

```
You want to validate a narrative index for a new domain.
│
├─ Do you have external time-series data?
│   ├─ YES → Concurrent + Predictive validation
│   │         (correlation, Granger causality, VAR)
│   └─ NO → Go to next question
│
├─ Are there known shock events in the domain?
│   ├─ YES → Event study validation
│   │         (pre/post index change around shocks)
│   └─ NO → Go to next question
│
├─ Can you survey experts or the public?
│   ├─ YES → Expert elicitation or survey comparison
│   └─ NO → Go to next question
│
├─ Are there multiple news sources?
│   ├─ YES → Source consistency + convergent/discriminant validation
│   └─ NO → Go to next question
│
└─ Fallback: Content validity + inter-annotator agreement + temporal consistency
             (weakest but still valid for a preliminary index)
```

**Every domain has at least 2–3 validation pathways.** The question is which are feasible given data availability.

---

## 5. Why Economics Is Unusually Easy (and what to learn from it)

Economics is the **easiest domain** for narrative index validation. This is not a weakness of other domains — it's a design constraint.

| Advantage | Economics | Other Domains | Mitigation |
|-----------|-----------|---------------|------------|
| **Data frequency** | Monthly CPI, daily FX | Often annual or quarterly | Use event studies + source consistency as primary validation |
| **Data precision** | Well-measured, audited | Often survey-based, noisy | Use multiple weak signals + triangulation |
| **Temporal coverage** | Decades (30+ years) | Often patchy, inconsistent | Bootstrap with event studies first; add time-series as data accumulates |
| **Theory** | Clear causal mechanisms (Shiller, 2017) | Often contested or emerging | Be transparent: "we are measuring what is said, not proving what drives outcomes" |
| **Lag structure** | Well-understood (2–6 months) | Domain-dependent | Compute cross-correlation functions empirically |
| **Policy relevance** | Central banks actively use nowcasts | Often aspirational | Publish as a "discourse index" not a "predictive index" initially |

---

## 6. The Honest Communication Principle

When publishing or presenting a narrative index, always be transparent about which validation levels you achieved:

> **Good:** "Our Health Narrative Index for Bangla news achieves inter-annotator agreement of κ = 0.73 and passes 8/12 event study tests (spiking during COVID waves, dengue outbreaks, and healthcare strikes). Concurrent validation against hospital admission data is limited by data availability but shows r = 0.45 for the available 24-month window."

> **Better than good — also note what you couldn't do:** "We were unable to test Granger causality due to the annual frequency of the available health outcome data. This is a limitation we acknowledge. The index remains useful as a high-frequency discourse measure even without causal validation."

---

## 7. Quick Reference: External Data Sources by Domain

| Domain | Primary Sources | Universal Sources |
|--------|----------------|-------------------|
| **Health** | WHO, national health ministries, CDC, IHME (GBD), Johns Hopkins CSSE | Event studies (known outbreaks), survey data (Gallup) |
| **Climate** | NOAA, NASA, IPCC, EM-DAT, national meteorological agencies | Event studies (disasters), weather records |
| **Education** | UNESCO, World Bank EdStats, OECD PISA, national ministries | Event studies (policy reforms, strikes) |
| **Governance** | World Bank WGI, Transparency International, Gallup, V-Dem | Event studies (elections, scandals, protests) |
| **Social** | World Bank, ILO, UNU-WIDER, ACLED (protests) | Event studies (court rulings, movements) |
| **Technology** | ITU, GSMA, Crunchbase, OECD Digital Economy | Event studies (product launches, breaches) |
| **All domains** | — | Expert elicitation, source diversity checks, temporal consistency |

---

*This framework is designed to complement the LILA Lab XENI pipeline methodology. For the specific BENI economic narrative validation pipeline, see `presentations/RESEARCH_PRESENTATION.md`. For narrative extraction methodology fundamentals, see `presentations/NARRATIVE_EXTRACTION_SYSTEMS.md`.*

*Last updated: June 2026*
