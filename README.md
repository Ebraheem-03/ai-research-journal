# 🧠 AI Research Journal

> **An automated, zero-cost AI/ML research journal and learning ledger — powered entirely by GitHub Actions, Tavily, and Groq.**

![Automated](https://img.shields.io/badge/Automated-GitHub_Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white)
![Zero Cost](https://img.shields.io/badge/Zero_Cost-Free_Tier_Only-00C853?style=flat-square)
![LLMOps Grade](https://img.shields.io/badge/LLMOps-Production_Grade-7C3AED?style=flat-square)
![Recruiter Friendly](https://img.shields.io/badge/Recruiter-Friendly-FF6F00?style=flat-square)

---

## What This Is

This repository is a **fully automated AI research journal** that runs itself — every day, every week, every month — with zero manual intervention. It tracks real developments across the 2025–2026 AI stack and produces technically defensible research notes grounded in actual papers, blog posts, and engineering reports.

It is **not** a fake activity generator. Every commit reflects a genuine file change. Every weekly entry cites a real source. Every daily log entry maps to a concrete AI engineering activity.

---

## How It Works

```
┌──────────────┐     ┌────────────┐     ┌────────────┐     ┌──────────────┐
│ GitHub Actions│────▶│ Tavily API │────▶│  Groq API  │────▶│  Markdown    │
│  (Scheduler)  │     │  (Search)  │     │  (LLM)     │     │  (Output)    │
└──────────────┘     └────────────┘     └────────────┘     └──────────────┘
       │                                                           │
       │              Daily / Weekly / Monthly                     │
       └───────────────── git commit + push ◀──────────────────────┘
```

| Pipeline | Schedule | What It Does |
|----------|----------|--------------|
| **Daily** | 08:00 UTC, every day | Appends a specific AI engineering activity to `daily_log.md` |
| **Weekly** | 09:00 UTC, every Sunday | Searches for a real AI paper/blog via Tavily, generates a structured research note via Groq, appends to `weekly_ai_notes.md` |
| **Monthly** | 10:00 UTC, 1st of each month | Aggregates stats, extracts themes, produces a digest in `monthly_digest.md` |

### Stack

- **GitHub Actions** — orchestration, scheduling, CI/CD
- **Tavily API (Free Tier)** — real-time search for AI research content
- **Groq API (Free Tier)** — fast LLM inference (Llama 3.3 70B) for summary generation
- **Python 3.11+** — inline scripting on GitHub-hosted runners
- **jq** — lightweight JSON manipulation for stats tracking

---

## Technical Focus Areas

Each week, the research pipeline rotates through these topics:

### 🏗️ Large Language Models (LLMs)
Architecture evolution, context window scaling, Mixture-of-Experts (MoE), open-weight models (DeepSeek-R2, Qwen3, Llama 4), inference efficiency, and structured output generation.

### 🔍 Retrieval-Augmented Generation (RAG)
Chunking strategies (semantic, late, agentic), vector database benchmarking (Pinecone, Milvus, Qdrant), hybrid search (BM25 + dense), re-ranking (ColBERT, cross-encoders), and Reciprocal Rank Fusion.

### 🤖 Agentic AI Systems
Multi-agent orchestration (LangGraph, AutoGen, CrewAI), tool use, Agent-to-Agent (A2A) protocol, Model Context Protocol (MCP), human-in-the-loop checkpoints, and token budget management.

### ⚙️ LLMOps & MLOps
Prompt versioning, hallucination detection (SelfCheckGPT, NLI-based), evaluation pipelines (RAGAS, LangSmith), CI/CD for AI systems, regression testing for prompt changes, and production tracing.

### 📏 AI Evaluation
LLM-as-a-Judge frameworks, RAGAS metrics (faithfulness, context recall), benchmarks (GPQA, MMLU, HumanEval), red-teaming methodologies, and evaluation-driven development.

### 🛡️ AI Safety & Alignment
RLHF, Constitutional AI, Guardrails-AI, NIST AI RMF 1.0, responsible scaling policies, output filtering, and adversarial robustness.

---

## 2026 Trends Tracked

This journal keeps pace with the key themes shaping the AI landscape in 2026:

- **Reasoning models** — Chain-of-thought at scale (DeepSeek-R2, o3-mini), verifiable reasoning traces
- **Edge AI** — On-device inference, quantized models (GGUF, AWQ), mobile deployment
- **Sovereign AI** — National AI infrastructure, data residency, region-specific model hosting
- **Open-source model parity** — Open-weight models matching proprietary performance (Llama 4, Qwen3, Mistral Large)
- **Agentic infrastructure** — Production-grade agent frameworks, reliability patterns, observability
- **AI evaluation maturity** — Moving beyond vibes-based eval to systematic, automated quality gates

---

## Repository Structure

```
ai-research-journal/
├── README.md              ← You are here
├── daily_log.md           ← Append-only daily engineering activities
├── weekly_ai_notes.md     ← Structured weekly research notes (centrepiece)
├── monthly_digest.md      ← Monthly aggregated digest
├── stats.json             ← Pipeline state and statistics
└── .github/
    └── workflows/
        ├── daily.yml      ← Daily log automation
        ├── weekly.yml     ← Weekly research pipeline (Tavily → Groq)
        └── monthly.yml    ← Monthly digest generator
```

---

## Setup

1. Fork or clone this repository
2. Add the following secrets in **Settings → Secrets and Variables → Actions**:
   - `TAVILY_API_KEY` — [Get a free key](https://tavily.com)
   - `GROQ_API_KEY` — [Get a free key](https://console.groq.com)
3. Enable GitHub Actions in the **Actions** tab
4. Done. The system runs itself.

### Cost

| Service | Free Tier Limit | This Repo's Usage |
|---------|----------------|-------------------|
| GitHub Actions | Unlimited (public repos) | ~3 runs/week |
| Tavily | 1,000 searches/month | ~4 searches/month |
| Groq | ~14,400 requests/day | ~4 requests/month |

**Total cost: $0/month. Forever.**

---

## Quality Standard

Every entry in this journal is designed to withstand scrutiny. A reviewer should conclude:

> *"This engineer documents what they're learning, automates intelligently, understands the current AI stack, and can discuss LLMOps, RAG, and agentic systems fluently."*

---

## License

MIT
