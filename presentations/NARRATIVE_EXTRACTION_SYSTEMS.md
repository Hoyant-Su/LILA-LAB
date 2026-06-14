# Narrative Extraction Systems — From Basic to Intermediate
## A Conceptual Primer for Researchers

---

> **Narrative extraction** is the process of identifying, measuring, and tracking stories, frames, and themes from text. In economics, it answers: *"What are people talking about, and does it matter for real-world outcomes?"*

This document explains the major families of narrative extraction methods — how they work, what they're good at, where they break, and how they connect to the LILA Lab pipeline framework.

---

## Table of Contents

1. [What Is a Narrative?](#1-what-is-a-narrative)
2. [Why Extract Narratives?](#2-why-extract-narratives)
3. [The Method Spectrum](#3-the-method-spectrum)
4. [Dictionary-Based Methods](#4-dictionary-based-methods)
5. [Topic Modeling](#5-topic-modeling)
6. [Supervised Text Classification](#6-supervised-text-classification)
7. [Word Embeddings & Vector Semantics](#7-word-embeddings--vector-semantics)
8. [Transformer-Based Models](#8-transformer-based-models)
9. [LLM-Based Annotation](#9-llm-based-annotation)
10. [LLM Ensembles & Adjudication](#10-llm-ensembles--adjudication)
11. [Active Learning](#11-active-learning)
12. [Hybrid Pipelines (LILA Lab's Approach)](#12-hybrid-pipelines-lila-labs-approach)
13. [Choosing the Right Method](#13-choosing-the-right-method)
14. [Limitations & Pitfalls](#14-limitations--pitfalls)
15. [Further Reading](#15-further-reading)

---

## 1. What Is a Narrative?

A **narrative** is more than a topic. It's a **story with structure** — actors, actions, causality, and evaluation.

| Concept | Definition | Example |
|---------|-----------|---------|
| **Topic** | What the text is about | "Inflation" |
| **Narrative** | The story being told about the topic | "Rising inflation is caused by supply chain disruptions and is hurting poor households the most" |
| **Frame** | The angle, perspective, or interpretive lens | Economic hardship frame vs. policy failure frame vs. global phenomenon frame |
| **Sentiment** | Emotional valence | Negative (fear/anxiety), neutral, positive (optimism) |
| **Narrative index** | A time-series measure of narrative prevalence | "Share of news articles expressing economic anxiety, aggregated monthly" |

**Key insight:** Two articles can be about the same topic but carry completely different narratives. "Inflation is transitory" vs. "Inflation is permanent structural damage" — same topic, opposing narratives.

### The Narrative Extraction Pipeline (Conceptual)

```
Raw Text → Preprocessing → Narrative Signal Detection → Classification/Measurement → Aggregation → Validation
```

---

## 2. Why Extract Narratives?

Narratives matter because they **shape expectations, behavior, and decisions**.

| Domain | Narrative Question | Real-World Impact |
|--------|-------------------|-------------------|
| **Economics** | "Are news stories about inflation increasing?" | Inflation expectations → actual inflation (self-fulfilling) |
| **Health** | "Is the public discourse around vaccines becoming more skeptical?" | Vaccination rates |
| **Climate** | "Are climate narratives shifting from 'future risk' to 'current crisis'?" | Policy urgency, public behavior |
| **Politics** | "How is immigration being framed across media outlets?" | Voting behavior, policy preferences |
| **Finance** | "What narratives dominate earnings calls?" | Stock price movements |

**The core premise (Shiller, 2017):** Narratives spread like viruses and drive economic outcomes that cannot be explained by fundamentals alone. If you can measure narratives, you can **nowcast** (predict the present) and potentially **forecast** future behavior.

---

## 3. The Method Spectrum

Narrative extraction methods exist on a spectrum from **fully manual** to **fully automated**:

```
Manual        Dictionary     Topic        Supervised    Embeddings    Transformers    LLM-based
Coding        Methods        Modeling     ML                                          Systems
    │             │              │             │             │              │             │
    ▼             ▼              ▼             ▼             ▼              ▼             ▼
 1916s         1960s          2003         2000s         2013           2018           2022

Low ▲━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━► High
Cost                                                                                
Low ◀━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━► High Automation
Low ◀━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━► High Scale
High◀━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━► Low Depth
```

| Method | Human Effort | Scale | Interpretability | Reliability | Cost |
|--------|-------------|-------|-----------------|-------------|------|
| Manual coding | Very high | Very low | Very high | High | Very high |
| Dictionary | Low | Very high | High | Low-Medium | Very low |
| Topic Modeling | Low | Very high | Medium | Low-Medium | Very low |
| Supervised ML | Medium | High | Medium | High | Low |
| Embeddings | Low | High | Low | Medium | Low |
| Transformers | Medium | High | Low-Medium | High | Medium |
| LLM-based | Low-Medium | High | Medium | Medium-High | Medium-High |

---

## 4. Dictionary-Based Methods

### What They Are

A **dictionary** (also called a **lexicon**) is a list of words or phrases associated with a concept. To measure a narrative, you count how many dictionary words appear in a text.

### How They Work

```
Dictionary: {"inflation", "prices", "cost of living", "CPI", "inflationary"}
    
Text: "The rising cost of living is putting pressure on household budgets as inflation surges"
      └──────────┬─────────┘                        └─────┬──────┘
              "cost of living" ✓                       "inflation" ✓
      
Score = 2 matches / 10 words = 0.20 (20% narrative density)
```

### Famous Dictionaries

| Dictionary | Purpose | Words | Used In |
|-----------|---------|-------|---------|
| **Loughran-McDonald** | Financial sentiment | ~80K words | Finance, accounting research |
| **Harvard IV-4** | General sentiment | ~4K words | Social science |
| **LIWC** | Linguistic inquiry | ~6,400 categories | Psychology, sociology |
| **General Inquirer** | General purpose | ~11K words | Classic content analysis |

### Pros & Cons

| ✅ Strengths | ❌ Weaknesses |
|-------------|---------------|
| Extremely simple to understand and implement | Cannot handle context or polysemy ("bank" = river vs. financial) |
| Fully reproducible (same dictionary = same results, always) | Misses sarcasm, irony, negation ("not good" = negative, not positive) |
| Computationally trivial (word counting) | Language-specific (need a new dictionary for each language) |
| Works at massive scale (millions of documents) | Cannot capture complex narratives — only keywords |
| Perfect for well-defined, stable concepts | Dictionary decays over time (words change meaning) |

### When to Use

- **Pilot studies** where you need a quick, transparent first pass
- **Well-defined concepts** with stable vocabulary ("inflation", "unemployment")
- **Replication** where methodological simplicity is a virtue
- **Baseline comparison** to demonstrate that more sophisticated methods add value

### LILA Lab Context

LILA Lab treats dictionary methods as **Level 2** on the 12-level methodology hierarchy. BENI's TF-IDF classifier implicitly learns a weighting scheme that approximates a data-driven dictionary — but with contextual awareness.

---

## 5. Topic Modeling

### What It Is

Topic modeling discovers **latent themes** ("topics") that run through a collection of documents — **unsupervised**, meaning no labeled data required. The algorithm infers structure from word co-occurrence patterns.

### How It Works (LDA — Latent Dirichlet Allocation)

**Intuition:** Every document is a mixture of topics. Every topic is a distribution over words.

```
                       ┌─────────────────────┐
                       │     Document 1       │
                       │  60% Topic A         │
                       │  30% Topic B         │
                       │  10% Topic C         │
                       └─────────────────────┘

Topic A: {inflation: 0.08, prices: 0.06, economy: 0.05, ...}
Topic B: {election: 0.07, vote: 0.05, candidate: 0.04, ...}
Topic C: {health: 0.06, hospital: 0.04, disease: 0.03, ...}
```

**The generative story (simplified):**

1. For each document, pick a distribution of topics
2. For each word in the document, pick a topic from that distribution
3. Pick a word from that topic's word distribution
4. Work backwards to infer the most likely topic structure given the observed words

### LDA in Practice

```
Input: 10,000 news articles
Output: 20 topics, each with top-10 words

Topic 7: inflation, prices, central bank, interest rate, economy, growth,...
Topic 12: election, vote, candidate, campaign, party, political,...
Topic 15: health, hospital, doctor, patient, disease, medical,...

→ Researcher assigns labels: Topic 7 = "Monetary Policy", Topic 12 = "Elections", Topic 15 = "Healthcare"
→ Track proportion of Topic 7 over time → "Economic narrative prevalence time series"
```

### Extensions of LDA

| Variant | What It Adds | Use Case |
|---------|-------------|----------|
| **Dynamic Topic Models (DTM)** | Topics evolve over time | Track how "inflation" topic changes 2010→2020 |
| **Structural Topic Models (STM)** | Include metadata (date, source, author) | "Do left-wing papers discuss inflation differently?" |
| **Correlated Topic Models (CTM)** | Topics can correlate | "Economic topics and political topics co-occur" |
| **BERTopic** | Uses transformer embeddings | More coherent topics, less preprocessing |

### Pros & Cons

| ✅ Strengths | ❌ Weaknesses |
|-------------|---------------|
| Fully unsupervised — no labeled data needed | Topics are statistical artifacts, not necessarily meaningful |
| Discovers unexpected patterns | Requires human interpretation ("What does this topic mean?") |
| Scalable to millions of documents | Stability issues (different runs = different topics) |
| Provides both document-level and corpus-level views | Difficult to validate — no ground truth |
| Good for exploration and hypothesis generation | Cannot capture framing, stance, or complex narratives |

### When to Use

- **Exploratory analysis** — "What themes exist in this corpus?"
- **Corpus overview** — understand the landscape before deeper analysis
- **Hypothesis generation** — find patterns you didn't know to look for
- **Low-resource settings** — no labeled data available

### When NOT to Use

- **Causal inference** — topics don't measure well-defined constructs
- **Replication** — different seeds, different topics
- **Policy-relevant measurement** — too unstable for decision-making

---

## 6. Supervised Text Classification

### What It Is

Supervised classification trains a model to assign labels to text using **human-annotated examples**. The model learns patterns from labeled data and generalizes to unseen text.

### How It Works

```
Phase 1: Training

Human annotator labels 5,000 articles:
    "Economic"     ← article about inflation and interest rates
    "Not Economic" ← article about a cricket match
    "Economic"     ← article about export tariffs
    ...

    │
    ▼

Model learns: words like "inflation", "GDP", "exports", "central bank" → "Economic"
              words like "cricket", "film", "recipe", "weather" → "Not Economic"

Phase 2: Inference

Unlabeled article: "The stock market fell sharply after the central bank raised rates"
    → Model predicts: "Economic" (confidence: 94%)
```

### Common Algorithms (from simple to complex)

| Model | How It Works | When to Use |
|-------|-------------|-------------|
| **Naive Bayes** | Word probabilities assuming independence | Small data, strong baselines |
| **Logistic Regression** | Weighted combination of word features | Best simplicity/performance tradeoff |
| **Support Vector Machine (SVM)** | Finds optimal decision boundary | High-dimensional text data |
| **Random Forest** | Ensemble of decision trees | When features are heterogeneous |
| **TF-IDF + Logistic Regression** | Weight words by importance (rare words weighted higher) | **Best baseline for text classification** |

### TF-IDF Explained (Critical for LILA Lab)

**TF-IDF** = Term Frequency × Inverse Document Frequency

```
Term Frequency (TF) = How often word W appears in document D
                     (normalized by document length)

Inverse Document Frequency (IDF) = log(Total documents / Documents containing W)
                     (rare words get higher weight, common words lower)

Example:
  Word "the" appears in 99% of documents → IDF ≈ 0 → TF-IDF ≈ 0 (ignored)
  Word "inflation" appears in 2% of documents → IDF ≈ 3.9 → high TF-IDF (signal)
  Word "Bangladesh" appears in 15% of documents → IDF ≈ 1.9 → medium TF-IDF
```

**Why TF-IDF is surprisingly effective:** It automatically filters out common words ("the", "and", "is") and highlights distinctive words — exactly what you want for narrative detection. The LILA Lab BENI pipeline achieves 91.7% accuracy with TF-IDF + Logistic Regression, beating even fine-tuned BanglaBERT.

### The CountVectorizer Pipeline (Visual)

```
Raw text → Tokenizer → CountVectorizer → TF-IDF Transformer → Classifier → Prediction
                              │                    │
                         Word frequency         Weight rare words
                         matrix (10K×50K)       higher (TF-IDF)
```

### Pros & Cons

| ✅ Strengths | ❌ Weaknesses |
|-------------|---------------|
| Clear, interpretable model (you can see which words matter most) | Requires large labeled datasets |
| High accuracy for well-defined categories | Domain-specific (model trained on economics may fail on health) |
| Fast training and inference | Cannot capture context beyond bag-of-words |
| Easy to debug and improve | Language-specific (features are words in that language) |
| Reproducible and deterministic | Static (captures patterns at training time, may drift) |

### When to Use

- **Well-defined categories** with clear boundaries ("Economic" vs "Not Economic")
- **Sufficient labeled data** (>1,000 examples per class)
- **Stable concepts** that don't change meaning over time
- **Production systems** requiring speed and reliability

---

## 7. Word Embeddings & Vector Semantics

### What They Are

Word embeddings represent words as **dense vectors in a high-dimensional space** — typically 100–300 dimensions. Words with similar meanings are closer together in this space.

### How They Work

**The key insight:** "You shall know a word by the company it keeps" (Firth, 1957)

```
"inflation" → [0.23, -0.45, 0.67, 0.12, ..., -0.03]  (300 numbers)
"prices"    → [0.21, -0.42, 0.65, 0.15, ..., -0.01]  (similar vector)
"cricket"   → [-0.34, 0.56, -0.12, 0.78, ..., 0.45]  (different vector)

Vector arithmetic:
  "king" - "man" + "woman" ≈ "queen"  (analogy!)
  "inflation" - "prices" + "jobs" ≈ "unemployment"
```

### Major Embedding Methods

| Method | Year | How It Works | Best For |
|--------|------|-------------|----------|
| **Word2Vec** | 2013 | Predicts a word from its neighbors (CBOW) or neighbors from a word (Skip-gram) | General word similarity |
| **GloVe** | 2014 | Factorizes word co-occurrence matrix | Global word statistics |
| **FastText** | 2016 | Like Word2Vec but uses character n-grams (handles unseen words) | Morphologically rich languages like Bengali |
| **Doc2Vec** | 2014 | Extends Word2Vec to whole documents | Document similarity, not just words |

### Using Embeddings for Narrative Extraction

**Method 1: Document Embedding Averaging**
```
Average all word vectors in a document → document vector
Compare document vectors to "economic narrative" prototype vector
→ Cosine similarity score = economic narrative intensity
```

**Method 2: Embedding + Classifier**
```
Word vectors → Document vector (averaged) → Logistic Regression → Classification
```

**Method 3: Semantic Similarity Search**
```
Query: "stories about economic hardship"
→ Find documents with closest embedding vectors
→ Rank by similarity score
→ Track proportion over time
```

### Pros & Cons

| ✅ Strengths | ❌ Weaknesses |
|-------------|---------------|
| Captures semantic relationships between words | Computationally expensive to train from scratch |
| Handles synonyms ("inflation" ≈ "price rise") | Out-of-vocabulary words in new domains |
| Enables cross-lingual transfer (aligned embeddings) | Black box — hard to interpret why two documents are "similar" |
| Reduces dimensionality (300 numbers vs 50,000 words) | Static embeddings don't handle polysemy well |

### Why LILA Lab Uses TF-IDF Over Embeddings

TF-IDF captures **discriminative words** better for binary relevance classification. Embeddings excel at **semantic similarity** but add complexity without accuracy gains for the "Economic vs Not Economic" task. As LILA Lab moves to **cross-lingual transfer** (training on Bangla, predicting on Assamese), aligned embeddings become more relevant.

---

## 8. Transformer-Based Models

### What They Are

Transformers are neural network architectures that process **entire sequences at once** (not word-by-word) and use **attention mechanisms** to weigh the importance of different words relative to each other.

### The Key Innovation: Self-Attention

```
Input: "The bank raised interest rates because the economy was overheating."

Attention weights for "economy":
    economy → bank: 0.15   (context: which bank?)
    economy → interest: 0.25  (context: monetary policy)
    economy → rates: 0.28   (strong connection)
    economy → overheating: 0.32  (strongest connection — causal link!)
```

Unlike word embeddings (which give each word ONE static vector), transformers give each word a **context-dependent representation**. "Bank" in "central bank" vs. "river bank" gets different vectors.

### Major Transformer Models

| Model | Year | Parameters | Best For |
|-------|------|-----------|----------|
| **BERT** | 2018 | 110M–340M | Classification, NER, QA |
| **RoBERTa** | 2019 | 125M–355M | Improved BERT |
| **XLM-R** | 2019 | 279M–559M | Cross-lingual (100 languages) |
| **BanglaBERT** | 2021 | 110M | Bengali-specific (used in LILA Lab) |
| **mBERT** | 2018 | 110M | Multilingual (104 languages) |

### How Fine-Tuning Works

```
                          ┌─────────────────────┐
                          │  Pre-trained BERT    │
                          │  (trained on massive  │
                          │  general text corpus) │
                          └──────────┬──────────┘
                                     │
                     ┌───────────────┴───────────────┐
                     │     Fine-tuning (transfer)     │
                     │  Train on your labeled data    │
                     │  (e.g., 5,000 economic/not     │
                     │   economic articles)           │
                     └───────────────┬───────────────┘
                                     │
                          ┌──────────┴──────────┐
                          │   Fine-tuned Model   │
                          │  Economic Classifier │
                          │   (91.7% accuracy)   │
                          └─────────────────────┘
```

The pre-trained model already "knows" language structure. Fine-tuning teaches it your specific task with relatively little data.

### Why BERT-based Models Sometimes Underperform

In LILA Lab's BENI pipeline, **TF-IDF + Logistic Regression (91.7%) outperforms BanglaBERT (89.3%)**. Why?

| Reason | Explanation |
|--------|-------------|
| **Small training data** | BERT needs 10K+ examples to beat TF-IDF; BENI had ~3K |
| **Task simplicity** | "Economic vs Not Economic" is largely keyword-driven — TF-IDF captures this perfectly |
| **Domain vocabulary** | Economic terms like "inflation", "GDP", "repo rate" are highly discriminative — transformers don't add much |
| **Computational cost** | BERT is 100× more expensive than TF-IDF for marginal gain |

**Expected:** BanglaBERT will outperform TF-IDF with 70K+ training examples (experiments pending on Kaggle GPUs).

### Pros & Cons

| ✅ Strengths | ❌ Weaknesses |
|-------------|---------------|
| State-of-the-art accuracy on most NLP tasks | Computationally expensive (GPUs required) |
| Handles context, polysemy, and long-range dependencies | Requires large training datasets to beat simpler models |
| Pre-trained models are widely available | Black box — harder to interpret than TF-IDF |
| Multilingual models enable cross-lingual transfer | Fine-tuning is sensitive to hyperparameters |

---

## 9. LLM-Based Annotation

### What It Is

Instead of training a small classifier on human labels, use a **Large Language Model** (like Claude, GPT-4o, Llama) to directly annotate text based on a **prompt** describing the task.

### The Fundamental Shift

```
Traditional Supervised ML:                       LLM-Based Annotation:
                                                 
Human annotates 5,000 examples    ───           Write a prompt describing the task
        │                                          │
        ▼                                           ▼
Train a classifier               ───           Apply LLM directly to each article
        │                                          │
        ▼                                           ▼
Classifier predicts labels       ───           LLM returns labels + explanations
```

**No training. No labeled data required. Just a good prompt.**

### How It Works

```
PROMPT (given once to the LLM):
─────────────────────────────────
You are an economic narrative annotator. Read the following news article
and determine if it discusses economic issues. An article is "Economic"
if it mentions: inflation, prices, employment, trade, fiscal/monetary
policy, business, industry, agriculture, or infrastructure.

Respond with:
{
  "label": "economic" or "not_economic",
  "confidence": "high"/"medium"/"low",
  "reasoning": "Brief explanation"
}

ARTICLE: [full article text]
─────────────────────────────────

LLM RESPONSE:
{
  "label": "economic",
  "confidence": "high",
  "reasoning": "The article discusses rising inflation (CPI at 7.2%),
  interest rate policy from Bangladesh Bank, and impact on food prices."
}
```

### Prompt Engineering Basics

| Technique | What It Does | Example |
|-----------|-------------|---------|
| **Role assignment** | Sets the LLM's persona | "You are an expert economic annotator..." |
| **Task definition** | Clearly states the task | "Classify this article as economic or not economic" |
| **Label definitions** | Explains what each label means | "Economic = mentions inflation, prices, GDP, etc." |
| **Examples** | Few-shot demonstrations | "Example 1: ... → economic. Example 2: ... → not_economic" |
| **Output format** | Structured JSON | "Respond with JSON: {label, confidence, reasoning}" |
| **Edge case handling** | Addresses ambiguity | "If uncertain, label as 'uncertain'" |

### Zero-Shot vs Few-Shot

| Approach | Description | Accuracy | Cost |
|----------|-------------|----------|------|
| **Zero-shot** | Task description only | ~80–85% | Lowest |
| **Few-shot (3–5 examples)** | Task + 3–5 labeled examples | ~85–90% | Low |
| **Few-shot (10–20 examples)** | Task + 10–20 diverse examples | ~90–93% | Medium |
| **Chain-of-thought** | Task + examples + reasoning instructions | ~90–95% | Medium (more tokens) |

### Cost Comparison

| Method | Cost per 1,000 articles | Time | Quality |
|--------|------------------------|------|---------|
| Human annotation | $50–$200 | 2–4 weeks | Very high |
| LLM annotation (Claude) | $3–$8 | 10–30 minutes | High |
| LLM annotation (GPT-4o) | $5–$15 | 10–30 minutes | High |
| Fine-tuned classifier | $0.01–$0.10 | Seconds | High (if trained well) |

LLM annotation is **10–50× cheaper than human annotation** with comparable quality, and **100–300× faster**.

### Pros & Cons

| ✅ Strengths | ❌ Weaknesses |
|-------------|---------------|
| No training data required | LLM API cost at scale (100K+ articles) |
| Adaptable to any domain (change the prompt, not the model) | Prompt sensitivity (small prompt changes → different results) |
| Provides reasoning (not just labels) | LLM biases present in outputs |
| Fast setup (hours, not weeks) | Reproducibility concerns (non-deterministic) |
| Multilingual by default (Claude/GPT speak 50+ languages) | Proprietary models — no transparency |

### LILA Lab Context

LILA Lab uses LLM annotation as the **first pass labeling layer** in the BENI pipeline. Claude + GPT-4o ensemble labels 664,000 Bangla news articles. These labels then train a TF-IDF classifier that **distills the LLM's knowledge into a fast, cheap, reproducible model**.

---

## 10. LLM Ensembles & Adjudication

### Why an Ensemble?

Single LLMs have **systematic biases**:
- Claude tends to be **conservative** (more "not_economic" labels)
- GPT-4o tends to be **expansive** (more "economic" labels)
- Both make mistakes in different ways

An **ensemble** combines multiple LLMs to reduce bias and increase reliability.

### How Ensemble Annotation Works

```
Article: "Bangladesh Bank cuts repo rate to stimulate economy"

┌──────────────────┐      ┌──────────────────┐
│   Claude 3.5     │      │    GPT-4o        │
│ economic (0.92)  │      │ economic (0.95)   │
└────────┬─────────┘      └────────┬──────────┘
         │                         │
         └──────────┬──────────────┘
                    │
                    ▼
         ┌──────────────────────┐
         │  Ensemble Adjudicator │
         │                      │
         │  AGREEMENT: Both     │
         │  say "economic"      │
         │  → Final: economic   │
         │  (high confidence)   │
         └──────────────────────┘
```

### Adjudication Protocols

| Scenario | Both Agree | One Uncertain | Both Disagree | One Confident, Other Disagrees |
|----------|-----------|---------------|---------------|-------------------------------|
| **Majority vote** | Use majority | Use confident | Use tiebreaker (third LLM) | Use confident |
| **Weighted confidence** | Average scores | Weight by confidence | Use higher-confidence | Use higher-confidence |
| **Conservative** | Accept if both agree | Default to "not_economic" | Reject (manual review) | Default to "not_economic" |
| **LLM-as-judge** | Accept | Ask a third LLM to decide | Third LLM adjudicates | Third LLM reviews |

### LILA Lab's Ensemble Approach

```
┌─────────────────────────────────────────────────────────────┐
│                  3-LLM Kaggle Ensemble                      │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Article → Claude 3.5 Sonnet → {label, confidence, reasons} │
│          → GPT-4o         → {label, confidence, reasons}   │
│          → Claude 3 Haiku → {label, confidence, reasons}   │
│                                                             │
│  Ensemble aggregation:                                      │
│  ├── If 3/3 agree → accept with high confidence             │
│  ├── If 2/3 agree → accept with medium confidence           │
│  └── If 0/3 or 1/3 → reject (send to human adjudication)   │
│                                                             │
│  Result: ~87% agreement rate, <1% human review needed       │
└─────────────────────────────────────────────────────────────┘
```

### Measuring Ensemble Performance

| Metric | What It Measures | Good Benchmark |
|--------|-----------------|----------------|
| **Agreement rate** | % of articles where all LLMs agree | >80% |
| **Kappa coefficient** | Inter-annotator agreement (chance-corrected) | >0.7 (substantial) |
| **Human validation rate** | % of ensemble labels confirmed by humans | >90% |
| **Disagreement patterns** | Which articles cause disagreement | Identify schema ambiguities |

---

## 11. Active Learning

### What It Is

Active learning is a strategy that **selects the most informative unlabeled examples** to label next, rather than labeling randomly. This dramatically reduces the number of labels needed.

### The Core Idea

```
Random sampling: Label 5,000 random articles → 91% accuracy
Active learning:    Label 1,200 strategically → 91% accuracy
                                      ▲
                             80% fewer labels, same result!
```

### How Active Learning Selects Articles

**Uncertainty sampling** — the most common strategy:

```
Step 1: Train classifier on small labeled set (N=500)
Step 2: Apply to all unlabeled articles (N=100,000)
Step 3: Sort by prediction confidence (lowest first)

Most confident (easy):         Least confident (informative):
  "Inflation rises to 7.2%"      "Cultural festival draws crowds"
  → 99.9% economic               → 51% economic / 49% not_economic
  "Cricket team wins match"     "New policy announced"
  → 99.9% not_economic           → 55% not_economic / 45% economic
  "GDP growth at 6.5%"          "Community meeting held"
  → 99.5% economic               → 52% not_economic / 48% economic

Step 4: Label the least confident 100 articles
Step 5: Retrain classifier
Step 6: Repeat until accuracy plateaus
```

### Active Learning Visualized

```
Accuracy
  ▲
  │    Random Sampling
1.0 │                        ●───●───●───●───●───●───●───●
  │                  ●───●───●
  │            ●───●
0.9 │      ●───●
  │  ●───●
  │
  │    Active Learning
1.0 │         ●───●───●───●───●───●───●───●───●───●───●
  │   ●───●
  │ ●───●
0.9 │●
  │
  └──────────────────────────────────────────────────► Labels
      500    1,000    1,500    2,000    2,500    3,000
```

### Query Strategies

| Strategy | How It Works | Best For |
|----------|-------------|----------|
| **Uncertainty sampling** | Pick predictions closest to 50% | General purpose |
| **Margin sampling** | Pick predictions with smallest margin between top-2 classes | Multi-class problems |
| **Entropy sampling** | Pick predictions with highest entropy (most uncertainty) | Probabilistic models |
| **Query-by-committee** | Train multiple models, pick where they disagree most | Ensemble methods |
| **Diversity sampling** | Pick examples that are different from already-labeled ones | Coverage |

### LILA Lab's Active Learning Results

| Round | Labeled Examples | Accuracy | Cumulative Cost |
|-------|-----------------|----------|-----------------|
| 1 | 500 | 82.3% | $15 |
| 2 | 750 | 86.1% | $22 |
| 3 | 1,000 | 89.3% | $30 |
| 4 | 1,250 | 90.7% | $38 |
| 5 | 1,500 | 91.2% | $45 |
| 6 | 2,000 | 91.5% | $60 |
| 7 | 3,000 | 91.7% | $90 |

**Key insight:** 80% of the accuracy gain comes from the first 1,000 labels. Diminishing returns after 1,500.

---

## 12. Hybrid Pipelines (LILA Lab's Approach)

### The Best of All Worlds

LILA Lab's BENI pipeline combines **four methods** in a single pipeline:

```
┌──────────────────────────────────────────────────────────────────────┐
│                      LILA Lab Hybrid Pipeline                        │
├──────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  Stage 1: LLM Ensemble Annotation (Section 9+10)                    │
│  ┌──────────────────────────────────────────────────────────────┐   │
│  │ Claude 3.5 + GPT-4o → 664K articles labeled as economic/not │   │
│  │ Cost: ~$0.003/article     │   │
│  │ Agreement rate: 87%       │   │
│  └──────────────────────────────────────────────────────────────┘   │
│                              │                                       │
│                              ▼                                       │
│  Stage 2: Active Learning (Section 11)                              │
│  ┌──────────────────────────────────────────────────────────────┐   │
│  │ Iteratively selects most informative articles for LLM        │   │
│  │ re-annotation → reduces total LLM calls by ~60%              │   │
│  └──────────────────────────────────────────────────────────────┘   │
│                              │                                       │
│                              ▼                                       │
│  Stage 3: TF-IDF Classifier (Section 6)                             │
│  ┌──────────────────────────────────────────────────────────────┐   │
│  │ Trained on LLM labels → 91.7% accuracy on held-out test set │   │
│  │ Distills LLM knowledge into a fast, cheap, reproducible      │   │
│  │ model — runs on a laptop, no GPU, no API calls               │   │
│  └──────────────────────────────────────────────────────────────┘   │
│                              │                                       │
│                              ▼                                       │
│  Stage 4: Index Construction                                       │
│  ┌──────────────────────────────────────────────────────────────┐   │
│  │ Monthly aggregation → BENI Economic Index (79 months)        │   │
│  │ Detrended, seasonally adjusted, normalized                   │   │
│  └──────────────────────────────────────────────────────────────┘   │
│                              │                                       │
│                              ▼                                       │
│  Stage 5: Macroeconomic Validation (Section 6 of main doc)         │
│  ┌──────────────────────────────────────────────────────────────┐   │
│  │ Econometric testing against CPI, FX, reserves                │   │
│  │ r = −0.75, Granger causality, VAR forecasting                │   │
│  └──────────────────────────────────────────────────────────────┘   │
└──────────────────────────────────────────────────────────────────────┘
```

### Why This Hybrid Approach Wins

| Component | What It Contributes | Why It's Necessary |
|-----------|-------------------|-------------------|
| **LLM ensemble** | High-quality labels at scale without human annotation | No human annotators available for low-resource languages |
| **Active learning** | 60% reduction in LLM annotation costs | Makes scale economically viable |
| **TF-IDF classifier** | Distills LLM knowledge into fast, cheap, reproducible model | 10,000× cheaper than LLM for inference at scale |
| **Macro validation** | Proves the index has real-world predictive power | Scientifically validates the whole pipeline |

### The Distillation Analogy

Think of LLM knowledge as **crude oil**:
- LLM annotation = **extraction** (expensive but flexible)
- Active learning = **refining** (targeted extraction)
- TF-IDF classifier = **distillation** (cheap, fast, deployable)
- Narrative index = **fuel** (usable product)

---

## 13. Choosing the Right Method

### Decision Tree

```
What's your goal?
│
├── Explore unknown corpus
│   └── Topic Modeling (LDA/BERTopic)
│
├── Measure well-defined concept with labeled data
│   ├── < 1,000 labels → LLM annotation
│   ├── 1,000–10,000 labels → Supervised ML (TF-IDF)
│   └── > 10,000 labels → Transformer fine-tuning
│
├── Measure well-defined concept WITHOUT labeled data
│   ├── Simple concept → Dictionary methods
│   ├── Complex concept → LLM annotation
│   └── Cross-language → Multilingual LLM
│
├── Track evolving narratives over time
│   ├── With historical data → Dynamic Topic Models
│   └── With labeled data → Classifier + time-series aggregation
│
└── Cross-lingual comparison
    └── Multilingual embeddings + aligned classifiers
```

### Method Selection Matrix

| Your Situation | Recommended Method | Why |
|---------------|-------------------|-----|
| No labeled data, small budget | **Dictionary** | Free, simple, transparent |
| No labeled data, medium budget | **LLM zero-shot** | Fast setup, good quality |
| Some labeled data (500–5K) | **TF-IDF + LR** | Best accuracy per dollar |
| Lots of labeled data (10K+) | **BERT fine-tune** | SOTA accuracy |
| Need to discover themes | **LDA/BERTopic** | Unsupervised discovery |
| Production deployment | **Distilled TF-IDF** | Fast, cheap, reproducible |
| Low-resource language | **Multilingual LLM** | Works across languages |
| Causal inference | **Validated index (hybrid)** | Statistical rigor |

---

## 14. Limitations & Pitfalls

### Common Pitfalls in Narrative Extraction

#### 1. The Validity Gap
```
❌ A topic model discovers a "topic" of inflation-related words → 
   You assume this topic = "economic narrative"
✅ You validate: correlation with CPI, human review, predictive power
```

**Lesson:** A statistical pattern is not automatically a meaningful narrative.

#### 2. The Reproducibility Crisis
```
Run 1: LDA with seed=42 → Topic 3 = {inflation, prices, economy}
Run 2: LDA with seed=99 → Topic 3 = {bank, interest, rate}
```

**Lesson:** Unsupervised methods need multiple runs, seed control, and stability checks.

#### 3. Temporal Concept Drift
```
2015: "austerity" → fiscal conservatism, spending cuts
2020: "austerity" → pandemic response, stimulus withdrawal
```

**Lesson:** Words change meaning. A 2019 classifier may fail on 2024 text.

#### 4. Language Blindness
```
English: "The economy is sick" → metaphorical (economic hardship)
Bengali: "অর্থনীতি অসুস্থ" (orthoniti osustho) → same metaphor, different words

But:
English: "sick" → also "illness" domain
Bengali: "অসুস্থ" (osustho) → almost exclusively health

A dictionary translating "sick" → অসুস্থ would flag health articles as economic.
```

**Lesson:** Direct dictionary translation across languages introduces systematic errors.

#### 5. LLM Bias Amplification
```
LLM annotators:
- Over-label economic articles as "economic" (confirmation bias toward explicit economic terms)
- Under-label narratives that are implicitly economic (e.g., social unrest → economic causes)
- Show systematic differences between Claude and GPT-4o
```

**Lesson:** Ensemble methods and human validation are essential guardrails.

#### 6. The Aggregate Fallacy
```
Monthly index shows: "Economic narratives declining"
But: Some outlets declining, others stable, one rising
Aggregation hides heterogeneity.
```

**Lesson:** Always check disaggregated patterns before trusting aggregates.

---

## 15. Further Reading

### Foundational Papers

| Paper | Contribution | Why Read It |
|-------|-------------|-------------|
| **Shiller (2017)** — "Narrative Economics" | Narrative contagion theory | Why narratives matter for economics |
| **Gentzkow et al. (2019)** — "Text as Data" | NLP for social science survey | Framework for text-as-data validation |
| **Grimmer & Stewart (2013)** — "Text as Data" | Best practices for automated content analysis | Validation philosophy |
| **Devlin et al. (2019)** — "BERT" | Transformer pre-training | Foundation of modern NLP |
| **Brown et al. (2020)** — "GPT-3" | LLM capabilities | Zero-shot / few-shot paradigm shift |

### Methods References

| Topic | Best Resource |
|-------|---------------|
| **Dictionary methods** | Loughran & McDonald (2011) — financial sentiment dictionaries |
| **Topic Modeling** | Blei (2012) — LDA review |
| **Supervised classification** | Manning et al. (2008) — "Introduction to Information Retrieval" |
| **Word embeddings** | Mikolov et al. (2013) — Word2Vec |
| **Transformers** | Vaswani et al. (2017) — "Attention Is All You Need" |
| **Active learning** | Settles (2009) — active learning survey |
| **Prompt engineering** | White et al. (2023) — prompt patterns |

### LILA Lab Resources

| Resource | Location | Content |
|----------|----------|---------|
| **BENI Pipeline** | `pipelines/BENI/` | Complete reference implementation |
| **Systematic Review** | `technical-reports/paper1_systematic_review/` | 66-paper literature review |
| **Methodology Hierarchy** | `docs/research/NARRATIVE_EXTRACTION_METHODOLOGIES.md` | 12-level framework |
| **Method Deep Dives** | `docs/research/methodologies/` | Level-by-level explanations |
| **BENI Pilot Manifest** | `docs/research/BENI_PILOT_RUN_MANIFEST.md` | Full experimental results |

---

## Glossary

| Term | Definition |
|------|-----------|
| **Narrative** | A story with structure — actors, actions, causality, and evaluation |
| **Frame** | The interpretive lens or angle of a narrative |
| **Narrative index** | A time-series measure of narrative prevalence in text |
| **Nowcasting** | Predicting the present (or very recent past) using alternative data |
| **TF-IDF** | Term Frequency × Inverse Document Frequency — word weighting scheme |
| **Bag-of-words** | Representing text as a multiset of words, ignoring order |
| **Embedding** | A dense vector representation of a word or document |
| **Attention** | A mechanism that weighs the importance of different input parts |
| **Fine-tuning** | Adapting a pre-trained model to a specific task |
| **Zero-shot** | Applying a model to a task it wasn't explicitly trained on |
| **Few-shot** | Providing a few examples in the prompt to guide the model |
| **Ensemble** | Combining multiple models to improve reliability |
| **Adjudication** | Resolving disagreements between multiple annotators |
| **Active learning** | Iteratively selecting the most informative examples to label |
| **Distillation** | Compressing knowledge from a large model into a smaller one |
| **Granger causality** | A statistical concept of predictive causality (X → Y if X precedes Y) |
| **Cointegration** | A statistical property of time series that move together in the long run |

---

*This primer covers Levels 1–8 of the LILA Lab 12-level narrative extraction hierarchy. For advanced topics (Levels 9–12: agentic extraction, multilingual transfer, cross-lingual alignment, self-improving systems), see the full methodology documentation at `docs/research/`.*

*Last updated: June 2026*
