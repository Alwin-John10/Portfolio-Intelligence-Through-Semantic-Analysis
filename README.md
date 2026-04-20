# Portfolio Intelligence Through Semantic Analysis

AI-powered portfolio intelligence platform that reclassifies public companies using semantic analysis, LLM summarization, vector embeddings, and self-healing MongoDB pipelines to uncover thematic investment opportunities beyond outdated sector labels.

---

## Overview

Traditional sector classification systems such as **GICS** and **BICS** were built for an earlier generation of markets. They often fail to capture how modern companies operate across multiple disruptive industries simultaneously.

For example:

* **Microsoft** is labeled as Software, but also has exposure to AI infrastructure, cloud computing, cybersecurity, and quantum research.
* **Tesla** is classified as Consumer Discretionary, yet it operates in robotics, batteries, autonomous systems, AI, and energy storage.
* **Amazon** is considered Consumer Services, while also being one of the world’s largest cloud infrastructure providers.

This project builds a next-generation investment intelligence engine that analyzes what companies actually do today rather than relying on static historical labels.

---

## Business Objective

Designed for a quantitative hedge fund environment, this platform identifies and ranks companies across emerging themes such as:

* AI Infrastructure & Semiconductors
* Cloud Computing & Data Centers
* Renewable / Nuclear Energy for Compute
* Crypto & Blockchain Infrastructure
* Quantum Computing
* Robotics & Autonomous Systems
* AI Cybersecurity
* Digital Finance & Fintech
* AR / VR / Metaverse Platforms
* Gene Editing & AI Healthcare

---

## Core Problem Solved

Legacy sector labels answer:

> “What industry was this company historically placed in?”

This platform answers:

> “What future technologies, markets, and structural growth themes is this company exposed to today?”

---

# System Architecture

---

## Part 1 — Self-Healing Data Warehouse Pipeline

Built a resilient multi-stage MongoDB pipeline that continuously enriches company intelligence data.

### Data Sources

* IWB ETF Holdings
* Wikipedia
* Bing Search + Selenium
* Yahoo Finance (`yfinance`)

### Multi-Pass Resolver Workflow

### Pass 1 — Wikipedia Resolver

* Uses Python `wikipedia` library
* Extracts company descriptions and infobox data
* Validates tickers using structured metadata

### Pass 2 — Bing Resolver

* Uses Bing + Selenium to locate unresolved company pages
* Recovers ambiguous or difficult company names

### Pass 3 — Yahoo Finance Resolver

* Final fallback for unresolved companies
* Pulls business summaries, sector, website, location, metadata

### Self-Healing Logic

Each MongoDB document stores progress flags.

Example:

```json
{
  "ticker": "MSFT",
  "wiki_resolver": "wikipedia",
  "summary_status": true,
  "embedding_status": true
}
```

If any step fails, rerunning the pipeline only processes missing records instead of rebuilding the full database.

### Result

* > 98% company coverage
* Modular and fault-tolerant architecture
* Production-style data warehouse design

---

## Part 2 — LLM Summarization Pipeline

Raw Wikipedia articles can exceed 10,000+ words and contain noise irrelevant to investing.

This stage converts long-form text into concise investable intelligence.

### Workflow

### Chunking Strategy

Large articles are split into manageable overlapping chunks.

### Map Step

LLM analyzes each chunk for:

* Strategic initiatives
* Product lines
* Growth themes
* Risks
* Competitive advantages

### Reduce Step

Chunk outputs are merged into final structured summaries.

### Final Output Fields

* Business Description
* Investment Exposure
* Industry Themes
* Material Insights

### Example

```json
{
  "company_name": "Microsoft",
  "investment_exposure": [
    "Cloud Infrastructure",
    "Artificial Intelligence",
    "Cybersecurity"
  ]
}
```

### Result

Structured company intelligence optimized for embeddings and search.

---

## Part 3 — Embedding Intelligence Layer

Transforms company summaries into semantic vectors for similarity search and clustering.

### Models Evaluated

* BAAI / BGE Small
* BAAI / BGE Large
* MPNet
* Nomic Embed Text

### Inputs Tested

* Raw Wikipedia Content
* LLM Summaries
* Chunked Aggregated Documents

### Evaluation Metrics

* Silhouette Score
* Cosine Similarity
* Sector Cluster Separation
* Market Relationship Validation

### Key Finding

LLM-generated summaries produced stronger semantic signal than raw long-form text.

### Result

Selected production-grade embedding model for search infrastructure.

---

## Part 4 — Hybrid Search Engine

Built a search system combining sparse keyword search with dense semantic retrieval.

---

### Sparse Search (BM25)

Best for:

* Exact keywords
* Tickers
* Specific terms

Example:

```text
quantum computing companies
```

---

### Dense Search (Vector Search)

Best for conceptual meaning.

Example:

```text
companies building next generation compute systems
```

---

### Hybrid Search (Reciprocal Rank Fusion)

Combines both systems for best overall performance.

### Example Queries

* AI chip manufacturers
* Cloud hyperscalers
* Robotics leaders
* Quantum hardware firms
* Fintech infrastructure providers

### Result

Hybrid retrieval outperformed standalone sparse or dense systems.

---

## Part 5 — Thematic Portfolio Construction & Backtesting

Used search outputs to build real investable baskets.

### Process

1. Query hybrid search engine
2. Retrieve candidate companies
3. Use LLM classifier:

* Core
* Secondary
* Not Relevant

4. Human review for final quality control
5. Build equal-weight portfolios
6. Backtest 5-year performance

---

### Example Themes

* AI Infrastructure
* Cloud Platforms
* Cybersecurity
* Quantum Computing
* Robotics
* Crypto Infrastructure
* Renewable Power for Compute

---

### Analytics Generated

* Cumulative Return Charts
* Theme vs Benchmark Comparison (QQQ / ARKK)
* Correlation Heatmaps
* Candlestick Portfolio Charts

---

## Tech Stack

* Python
* MongoDB Atlas
* Pandas / NumPy
* Scikit-Learn
* SentenceTransformers
* HuggingFace
* Ollama / LLMs
* Selenium
* BeautifulSoup
* Plotly
* Yahoo Finance API

---

## Key Features

* Self-healing production pipeline
* Multi-source data enrichment
* LLM-powered summarization
* Embedding model benchmarking
* Hybrid search engine
* Thematic portfolio generation
* Quantitative backtesting
* Human-in-the-loop validation

---

## Sample Use Cases

### Find Hidden AI Winners

Search:

```text
AI infrastructure software companies
```

Returns companies beyond obvious mega-caps.

### Detect Cross-Sector Opportunities

Identify industrial companies quietly building robotics or AI divisions.

### Build Custom Thematic ETFs

Generate portfolios for:

* Quantum Computing
* Energy Storage
* Digital Payments
* AI Healthcare

---

## Project Impact

This project demonstrates how AI can modernize traditional investment research by replacing outdated sector labels with dynamic semantic intelligence.

Instead of asking:

> “What sector is this company in?”

We ask:

> “What future trends will drive this company’s growth?”

---

## Final Takeaway

A hedge-fund style intelligence platform combining:

* Data Engineering
* NLP
* LLM Systems
* Search Infrastructure
* Quant Finance
* Portfolio Analytics

to generate actionable thematic investment insights.
