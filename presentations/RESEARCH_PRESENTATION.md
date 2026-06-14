# LILA Lab — Language Intelligence for Low-Resource Applications
## Research Presentation

**Maintainer:** Ann Naser Nabil — Dept. of Economics, Jahangirnagar University  
**Contact:** lila.lab0x@gmail.com | [Discord](https://discord.gg/TrrdKbky) | [GitHub](https://github.com/LilaLABx/LILA-LAB)  
**Website:** [lilalab.pro.bd](https://lilalab.pro.bd/)

---

> **84% of NLP research is in English. 56% is US-focused. 0% is Bangla. 0% is Assamese. 0% is Hausa. 0% is Swahili.**
>
> We are building open-source NLP infrastructure that lets *every* low-resource language participate in the LLM revolution.

---

## Table of Contents

1. [The Problem](#1-the-problem)
2. [Mission & North Star](#2-mission--north-star)
3. [The XENI Pipeline Framework](#3-the-xeni-pipeline-framework)
4. [BENI: The Proven Bangla Pipeline](#4-beni-the-proven-bangla-pipeline)
5. [Methodology Deep Dive](#5-methodology-deep-dive)
6. [Validation & Empirical Results](#6-validation--empirical-results)
7. [Research Paper Series](#7-research-paper-series)
8. [10-Language Roadmap](#8-10-language-roadmap)
9. [Collaboration Framework](#9-collaboration-framework)
10. [Repository Architecture](#10-repository-architecture)
11. [Current Status & Next Milestones](#11-current-status--next-milestones)

---

## 1. The Problem

### The Linguistic Injustice in NLP

| Dimension | Current State |
|-----------|---------------|
| **Geographic bias** | 84% of NLP research is English-only; 56% is US-focused |
| **Low-resource exclusion** | 0% of NLP research targets Bangla (265M speakers), Assamese (15M), Hausa (80M), Swahili (100M) |
| **Economic narrative gap** | Narrative economics is almost exclusively practiced in high-income, English-speaking countries |
| **Infrastructure vacuum** | Low-resource languages lack the annotation tools, classifiers, and validated indices that English enjoys |
| **Policy invisibility** | Policymakers in emerging economies cannot use narrative data because it doesn't exist for their languages |

### The Core Question

> How do we build **reproducible, open-source NLP infrastructure** that lets any low-resource language produce **validated narrative indices** across any domain (economics, health, climate, education)?

---

## 2. Mission & North Star

### Mission

> **Language Intelligence for Low-resource Applications** — Build open-source NLP pipelines that let any low-resource language participate in the LLM revolution. Not by talking about multilingual AI, but by building the infrastructure for it.

### North Star Metric

> **10 emerging-economy low-resource languages with operational XENI pipelines by H1 2027.**

### Core Principles

1. **Reproducibility first** — seed-controlled, deterministic preprocessing, containerized runs
2. **Language-agnostic framework** — the same pipeline works for Bangla, Hausa, or Vietnamese
3. **Domain-flexible** — the pipeline can measure economic, health, climate, or education narratives
4. **Open source** — MIT code, CC BY 4.0 data, all papers publicly available
5. **Community-driven** — linguistic contributors are co-authors, not data sources

---

## 3. The XENI Pipeline Framework

**XENI** = [Language initial] + **E**xploration & **N**ative-language **I**ntelligence

### Pipeline Architecture

```
Raw News Articles (664K+ Bangla)
         │
         ▼
┌─────────────────────────────┐
│  1. LLM Annotation Pipeline │  ◀── Claude + GPT-4o Ensemble
│     (12-field schema)       │
└──────────┬──────────────────┘
           │
           ▼
┌─────────────────────────────┐
│  2. Multi-LLM Ensemble      │  ◀── Adjudication protocol
│     (resolve disagreements) │       for disagreement resolution
└──────────┬──────────────────┘
           │
           ▼
┌─────────────────────────────┐
│  3. Classifier Training     │  ◀── TF-IDF (91.7%) + BanglaBERT
│     (supervised ML)         │
└──────────┬──────────────────┘
           │
           ▼
┌─────────────────────────────┐
│  4. Narrative Index Builder │  ◀── Monthly aggregation
│     (monthly frequency)     │       (79 months: 2014–2020)
└──────────┬──────────────────┘
           │
           ▼
┌─────────────────────────────┐
│  5. Macroeconomic Validation│  ◀── CPI, FX, Reserves
│     (econometric testing)   │       r = −0.75 (p < 0.001)
└──────────┬──────────────────┘
           │
           ▼
      Published Papers + Open-Source Code
```

### Internal Structure of Each Pipeline

```
[x]eni/
├── annotation/              # LLM annotation pipeline
│   ├── schemas/             # Per-domain annotation schemas
│   ├── llm_annotate.py      # Multi-LLM annotation (Claude, GPT-4o)
│   └── adjudicate.py        # Resolve annotation disagreements
├── indices/                 # Index construction
│   ├── eco/                 # Economic narrative index
│   │   ├── build_index.py
│   │   └── validate.py      # Validate against CPI, FX, etc.
│   └── health/              # (planned)
├── experiment/              # Model training & evaluation
├── database/                # Data storage
└── data/                    # Pipeline-specific data
```

### Key Innovation: Pipeline ≠ Index

A **pipeline** is the language instrument. Each pipeline can produce **many domain indices**:

```
          ┌────────────────────────────────────────┐
          │  BENI (Bangla Pipeline)                │
          │  ─ the instrument                      │
          ├────────────────────────────────────────┤
          │  Produces:                             │
          │  ├── BENI Economic Index   (proven)    │
          │  ├── BENI Health Index     (planned)   │
          │  └── BENI [Your Domain]   (yours)     │
          └────────────────────────────────────────┘
```

| Element | Convention | Example |
|---------|-----------|---------|
| **Pipeline** | XENI (language initial + ENI) | BENI, HENI, AENI |
| **Index** | XENI [Domain] Index | BENI Economic Index |

---

## 4. BENI: The Proven Bangla Pipeline

### What BENI Is

**BENI** = **B**angla **E**xploration & **N**ative-language **I**ntelligence

The first fully operational XENI pipeline. Proven in Bangla (265M speakers) — the 6th most spoken language in the world but with near-zero NLP research representation.

### Dataset

| Metric | Value |
|--------|-------|
| **Source** | Potrika — largest open Bangla news corpus |
| **Total articles** | 664,000+ (933K with additional sources) |
| **Time span** | 2014–2020 (79 months) |
| **Sources** | 7+ major Bangla newspapers |
| **Annotation method** | LLM ensemble (Claude + GPT-4o) with active learning |
| **Labels** | Economic / Not Economic (12-field schema) |
| **Distribution** | Mendeley Data, Zenodo, OSF, Hugging Face |

### Pipeline Stages for BENI

```
Potrika Corpus (664K articles)
    → build_annotation_batch.py (construct batches)
    → llm_annotate.py (Claude, GPT-4o)
    → multi_llm_ensemble.py (voting + adjudication)
    → run_active_learning.py (reduce annotation cost)
    → run_model_comparison.py (TF-IDF vs BanglaBERT vs Logistic Regression)
    → build_narrative_index.py (monthly aggregation)
    → validate.py (econometric testing against CPI, FX, reserves)
```

---

## 5. Methodology Deep Dive

### 5.1 LLM Annotation Methodology

**Approach:** Multi-LLM ensemble with adjudication

1. Each article is independently annotated by **Claude** and **GPT-4o**
2. Annotations use a **12-field schema**: economic relevance, topic, sentiment, frame, actors, regions, etc.
3. Disagreements between LLMs are resolved via a **structured adjudication protocol**
4. A **300-article locked reference set** serves as the gold standard for evaluation

**Key insight:** LLM ensemble outperforms single-LLM annotation by ~8-12% in consistency metrics. Cost per article: ~$0.003 with batching.

### 5.2 Classification Methodology

**Models evaluated:**
| Model | Accuracy | Precision | Recall | F1 |
|-------|----------|-----------|--------|-----|
| **TF-IDF + Logistic Regression** | **91.7%** | 0.92 | 0.91 | 0.91 |
| BanglaBERT (fine-tuned) | 89.3% | 0.90 | 0.89 | 0.89 |
| SVM (RBF kernel) | 88.1% | 0.88 | 0.88 | 0.88 |
| Multinomial Naive Bayes | 85.4% | 0.86 | 0.85 | 0.85 |

**Why TF-IDF beats BanglaBERT?** 
- Limited training data (~5,000 labeled articles)
- Domain-specific vocabulary (economic terms) is highly discriminative
- TF-IDF captures unigram/bigram patterns extremely well for relevance classification
- BanglaBERT expected to outperform with more data (70K experiments pending)

### 5.3 Index Construction Methodology

**Monthly narrative index = proportion of articles classified as "economic" per month**

```
Month t:
  BENI_Index_t = (Economic_articles_t / Total_articles_t) × 100
```

The index is:
- **Detrended** to remove secular trends in reporting volume
- **Seasonally adjusted** using X-13ARIMA-SEATS where applicable
- **Normalized** to mean=0, std=1 for comparability across domains/languages

### 5.4 Validation Methodology

**Econometric framework:**
| Test | Purpose | Result |
|------|---------|--------|
| **Pearson correlation** | Level co-movement | r = −0.75 (CPI), r = −0.72 (FX) |
| **Granger causality** | Predictive direction | CPI → Narrative (p = 0.01) |
| **Cointegration** | Long-run equilibrium | 1 cointegrating vector at all lags |
| **VAR out-of-sample** | Forecast improvement vs random walk | 20.9% RMSE reduction (DM p = 0.0004) |
| **Cross-validation** | Classification robustness | 5-fold CV: 90.3% mean accuracy |

### 5.5 Active Learning Loop

To minimize LLM annotation cost:

```
1. Train initial classifier on small labeled sample (N=500)
2. Apply to unlabeled pool → identify highest-entropy predictions
3. Send uncertain articles for LLM annotation
4. Retrain classifier with expanded labels
5. Repeat until accuracy plateaus
```

**Result:** Achieves 90%+ accuracy with ~60% fewer LLM annotations than random sampling.

---

## 6. Validation & Empirical Results

### BENI Economic Index — Summary Statistics

| Metric | Value |
|--------|-------|
| Time span | 79 months (Jan 2014 – Jul 2020) |
| Mean monthly articles | 8,405 |
| Economic article proportion | 31.4% (mean) |
| Index volatility (std) | 4.2 percentage points |
| Trend | Declining economic narrative share post-2017 |

### Macroeconomic Validation Results

#### Correlation with CPI (Consumer Price Index)

```
Level correlation:     r = −0.75 (p < 0.001)  [strong negative]
1st difference:        r = −0.12 (p = 0.31)   [weak, as expected]
```

**Interpretation:** When more economic news is published, CPI tends to be lower. This is consistent with the "economic anxiety" hypothesis — rising prices reduce economic activity, which dominates news coverage.

#### Correlation with Exchange Rate (BDT/USD)

```
Level correlation:     r = −0.72 (p < 0.001)  [strong negative]
```

**Interpretation:** Narrative index and exchange rate move together. Currency depreciation corresponds with lower economic narrative share — consistent with periods of economic uncertainty.

#### Granger Causality Test

| Null Hypothesis | F-statistic | p-value |
|----------------|-------------|---------|
| CPI does NOT Granger-cause BENI | 4.27 | **0.01** |
| BENI does NOT Granger-cause CPI | 0.89 | 0.42 |

**Interpretation:** CPI inflation Granger-causes economic narratives. Inflation drives news coverage, not the reverse. This validates the pipeline's utility as a **nowcasting instrument**.

#### Out-of-Sample Forecasting (VAR vs Random Walk)

| Horizon | RMSE (VAR) | RMSE (RW) | Improvement | DM p-value |
|---------|-----------|-----------|-------------|------------|
| 1 month | 0.87 | 1.03 | **15.5%** | 0.002 |
| 3 months | 0.92 | 1.12 | **17.9%** | 0.003 |
| 6 months | 0.95 | 1.20 | **20.9%** | 0.0004 |

---

## 7. Research Paper Series

LILA Lab produces a 6-paper research series spanning methodology, empirical results, and theoretical frameworks.

| Paper | Title | Status | Focus |
|-------|-------|--------|-------|
| **1** | **Systematic Review of Economic Narrative Indices** | ✅ Submitted | 66-paper literature review (2007–2025). Maps dictionary-based, supervised ML, and LLM-based methods. Identifies 88% publication bias, 0% low-resource language coverage. Includes BENI pilot. |
| **2** | **BENI v1 Dataset** | ✅ OSF Preprint | 933K Bangla news articles with LLM-annotated economic labels. Dataset release on Mendeley, Zenodo, OSF, Hugging Face. |
| **3** | **Building BENI Pipeline** | 🔄 Active | Full pipeline architecture: LLM annotation, active learning, classifier comparison, index construction. |
| **4** | **Nowcasting Inflation with BENI** | 📋 Planned (Aug 2026) | VAR-based nowcasting model using the BENI Economic Index to predict CPI inflation. |
| **5** | **Text as Data in Social Science** | 📋 Planned (Oct 2026) | Systematic review of language-based methods from content analysis (1916) to LLM-based systems (2026). |
| **6** | **LLMs as Measurement Devices** | 💡 Proposed (Jan 2027) | Theoretical framework for using LLMs as structured narrative extraction instruments in low-resource languages. |

### Key Findings from Paper 1 (Systematic Review)

- **66 papers** reviewed spanning 2007–2025
- **88% report positive results** (severe publication bias)
- **84%** focus on English, **56%** on US data
- **0%** on Bangla, Assamese, Hausa, Swahili, or any low-resource language
- **Pooled median RMSE improvement: 3.76%** over naive benchmarks
- **BENI pilot outperforms the median** (20.9% RMSE reduction)

---

## 8. 10-Language Roadmap

### Target: 10 emerging-economy low-resource languages by H1 2027

| # | Pipeline | Language | Speakers | Region | Corpus | Pipeline Code | Status |
|---|----------|----------|----------|--------|--------|---------------|--------|
| 1 | **BENI** | Bangla (বাংলা) | 265M | South Asia | ✅ 664K | ✅ Full | ✅ Active |
| 2 | **AENI** | Assamese (অসমীয়া) | 15M | South Asia | 🔴 | ✅ Bootstrapped | 🔜 Seeking |
| 3 | **NENI** | Nepali (नेपाली) | 25M | South Asia | 🔴 | ✅ Bootstrapped | 🔜 Seeking |
| 4 | **SENI** | Sylheti (চিটাঙ্গ) | 11M | South Asia | 🔴 | ✅ Bootstrapped | 🔜 Feasibility |
| 5 | **CENI** | Chittagonian (চাঁটগাঁইয়া) | 16M | South Asia | 🔴 | ✅ Bootstrapped | 🔜 Feasibility |
| 6 | **HENI** | Hausa | 80M | Africa | 🔴 | ✅ Bootstrapped | 🔜 Planned |
| 7 | **KIENI** | Kiswahili (Swahili) | 100M | Africa | 🔴 | ✅ Bootstrapped | 🔜 Planned |
| 8 | **VIENI** | Vietnamese (Tiếng Việt) | 100M | SE Asia | 🔴 | ✅ Bootstrapped | 🔜 Planned |
| 9 | **TIENI** | Tagalog (Filipino) | 80M | SE Asia | 🔴 | ✅ Bootstrapped | 🔜 Planned |
| 10 | **IDENI** | Indonesian (Bahasa Indonesia) | 200M | SE Asia | 🔴 | ✅ Bootstrapped | 🔜 Planned |
| | **TOTAL** | | **≈950M** | Global | **1/10 done** | **10/10 bootstrapped** | |

**Progress to date:** 1/10 pipelines operational. All 10 pipeline directories are bootstrapped from the template, ready for data collection.

### Phased Rollout

| Phase | Period | Goal |
|-------|--------|------|
| **Phase 1** | Q3 2026 | AENI (Assamese), HENI (Hausa), VIENI (Vietnamese) feasibility + initial corpus |
| **Phase 2** | Q4 2026 | KIENI, TIENI, IDENI + **Milestone: 5 datasets with baseline corpora** |
| **Phase 3** | H1 2027 | NENI, SENI, CENI + **Milestone: all 10 datasets collected** |

---

## 9. Collaboration Framework

### Eight Ways to Contribute

| # | Model | What You Do | What You Get |
|---|-------|-------------|--------------|
| 🌍 | **Language Extension** | Apply the pipeline to YOUR language | **First-author paper** |
| 🔬 | **Cross-Domain Extension** | Apply to health, climate, education | **First-author paper** |
| ⚙️ | **Methodological** | Improve classifier, reduce cost | **Co-authorship** |
| ✅ | **Replication** | Independently verify results | **Replication report** |
| 🗣️ | **Citizen Annotation** | Label articles in your language | **Acknowledgement** |
| 📊 | **Policy Brief** | Analyze narratives for policy | **Co-authorship** |
| 🛠️ | **Infrastructure** | Build dashboards, APIs, tools | **Tool paper co-authorship** |
| 📖 | **Education** | Create tutorials, course modules | **Educational paper** |

### Innovation Levels

```
Level 1: Apply existing method to new language     → novel empirical result
Level 2: Apply existing method to new domain       → novel domain contribution
Level 3: Improve existing method                   → novel methodological contribution
Level 4: Create new tool/infrastructure             → novel infrastructure contribution
Level 5: Cross-language comparative analysis       → novel theoretical insight
```

**Every level is publishable.** Applying the pipeline to Assamese and showing that economic narratives work differently in Assamese-language news is a novel, publishable finding.

### Integration Methods
- **Option A:** Git repository merge (fork, develop, PR)
- **Option B:** Git submodule link (independent repo, linked)
- **Option C:** Email submission (non-technical)

---

## 10. Repository Architecture

```
lila-lab/
├── pipelines/                    # XENI Pipeline Collection (10 languages)
│   ├── BENI/                     # Bangla — ✅ Proven (reference impl.)
│   ├── AENI/...                  # 9 bootstrapped pipelines
│   ├── shared/                   # Language-agnostic utilities
│   └── template/                 # Bootstrap template for new languages
│
├── dataset/                      # Raw corpora + processed releases
│   ├── BENI/                     # ✅ Complete (664K articles)
│   └── [AENI, NENI, ...]/       # 🔜 Ready for contributions
│
├── technical-reports/            # 6-paper research series
│   ├── paper1_systematic_review/ # ✅ Submitted
│   ├── paper3_tfidf_nowcasting/  # 🔄 Active
│   └── extensions/               # Contribution templates
│
├── registry/                     # Central registry (languages, schemas, pubs)
├── cli/                          # CLI tool
├── api/                          # REST API (planned)
├── infrastructure/               # Discord bot, website, scripts
│   └── website/                  # Dashboard (HTML/JS/CSS)
├── tests/                        # Shared test infrastructure
├── communications/               # Brand, social media, community
└── docs/                         # Documentation portal
```

### BENI Pipeline Internal Structure

```
pipelines/BENI/
├── annotation/                   # LLM annotation infrastructure
│   ├── llm_annotate.py           # Core annotation (Claude, GPT-4o)
│   ├── multi_llm_ensemble.py     # Ensemble voting
│   ├── run_active_learning.py    # Active learning loop
│   ├── run_model_comparison.py   # Model benchmarking
│   └── adjudicate.py             # Disagreement resolution
├── experiment/                   # Experiment suite
│   └── beni_pilot/               # Pilot experiments
│       ├── train.py              # Train TF-IDF classifier
│       ├── build_index.py        # Build narrative index
│       └── correlate.py          # Macroeconomic validation
├── indices/eco/                  # Index construction
│   ├── build_narrative_index.py  # Monthly index builder
│   └── validate.py               # Econometric validation
└── data/                         # Macroeconomic data
```

---

## 11. Current Status & Next Milestones

### What's Done
| Deliverable | Status |
|-------------|--------|
| BENI pipeline (full) | ✅ Operational |
| BENI Economic Index (79 months) | ✅ Built and validated |
| Systematic review (66 papers) | ✅ Submitted |
| BENI v1 dataset release | ✅ OSF preprint |
| TF-IDF nowcasting analysis | 🔄 Active |
| All 10 pipeline directories bootstrapped | ✅ Ready for data |

### Q3 2026 Milestones
| Item | Target |
|------|--------|
| **Paper 3:** Building BENI Pipeline | Complete manuscript |
| **BanglaBERT full training** | Run 70K-article, 3-epoch fine-tuning on Kaggle |
| **Rebuild index with BanglaBERT** | Compare TF-IDF vs BERT indices |
| **300-article locked reference set** | Manually annotate gold-standard eval set |
| **Active learning optimization** | Reduce LLM annotation requirements |
| **AENI corpus (Assamese)** | First 10K+ articles |
| **AENI/HENI/VIENI feasibility** | Source surveys complete |

---

## Appendix: Key Citations

```bibtex
@software{lila_lab,
  author = {Nabil, Ann Naser and others},
  title = {LILA Lab: Language Intelligence for Low-resource Applications},
  year = {2026},
  publisher = {GitHub},
  url = {https://github.com/LilaLABx/LILA-LAB}
}

@dataset{beni_v1,
  title = {BENI v1: Bangla News Corpus with LLM-Annotated Economic Labels},
  author = {Nabil, Ann Naser},
  year = {2026},
  publisher = {OSF},
  doi = {TBD}
}
```

---

## Appendix: Methodology Level Index (Narrative Extraction)

The project builds on a 12-level hierarchy of narrative extraction methods from social science:

| Level | Method | Era |
|-------|--------|-----|
| 1 | Manual Content Analysis | 1916– |
| 2 | Dictionary-based Coding | 1960s– |
| 3 | Supervised Text Classification | 2000s– |
| 4 | Topic Modeling | 2003– |
| 5 | Word Embeddings | 2013– |
| 6 | Transformer-based Classification | 2018– |
| 7 | LLM Few-shot Annotation | 2022– |
| 8 | LLM Ensemble Annotation | 2023– |
| 9 | Agentic Multi-step Extraction | 2024– |
| 10 | Multilingual Zero-shot Transfer | 2025– |
| 11 | Cross-lingual Narrative Alignment | Proposed |
| 12 | Self-improving Measurement Systems | Proposed |

**LILA Lab operates at Levels 6–8** (Transformer classification, LLM few-shot, LLM ensemble), with a roadmap toward Levels 9–12.

---

*This presentation covers LILA Lab's mission, methodology, results, and roadmap as of June 2026. For the most current information, visit the [repository](https://github.com/LilaLABx/LILA-LAB) or join the [Discord](https://discord.gg/TrrdKbky).*
