# Portfolio-Intelligence-Through-Semantic-Analysis
Advanced portfolio intelligence platform that reclassifies public companies using semantic analysis, Wikipedia enrichment, MongoDB pipelines, LLM summarization, and embeddings to uncover thematic investment opportunities beyond legacy sector labels.

## Overview

Traditional sector classifications such as GICS and BICS were designed for a different era of markets. They often fail to capture how modern companies are evolving across multiple industries.

For example:

- Microsoft is classified as Software, but is also deeply involved in AI infrastructure, quantum computing, and energy investments.
- Tesla is listed under Consumer Discretionary, yet it operates in robotics, autonomous systems, batteries, and AI.

This project builds an advanced company intelligence platform that uses **Wikipedia data, financial metadata, Large Language Models (LLMs), vector embeddings, and MongoDB pipelines** to identify investment opportunities hidden by outdated classifications.

---

## Business Objective

Designed for a quantitative hedge fund environment, this system helps build thematic portfolios across emerging industries:

- AI Infrastructure & Semiconductors
- Cloud Computing & Data Centers
- Nuclear / Renewable Energy for Compute
- Crypto & Blockchain Infrastructure
- Quantum Computing
- Robotics & Autonomous Systems
- AI Cybersecurity
- Digital Finance & Fintech
- AR / VR / Metaverse Platforms
- Gene Editing & AI Healthcare

---

## Core Problem Solved

Legacy sector labels answer:

> “What industry was this company in years ago?”

This project answers:

> “What technologies, markets, and future themes is this company exposed to today?”

---

# System Architecture

## Part 1 — Self-Healing Data Warehouse Pipeline

Build a resilient MongoDB data pipeline that continuously enriches company data.

### Data Sources

- IWB ETF Holdings
- Wikipedia
- Bing Search + Selenium
- Yahoo Finance (`yfinance`)

### Multi-Pass Resolver System

#### Pass 1 — Wikipedia Resolver
Uses Python Wikipedia library + infobox validation.

#### Pass 2 — Bing Resolver
Uses Bing search to find unresolved Wikipedia pages.

#### Pass 3 — Yahoo Finance Resolver
Fallback for companies without usable Wikipedia pages.

### Self-Healing Logic

Each company document stores status flags such as:

```json
{
  "ticker": "MSFT",
  "wiki_resolver": "wikipedia"
}
