# 📓 Weekly AI Research Notes

> Structured weekly research journal entries covering the 2025–2026 AI stack. Each entry is sourced from a real paper, blog post, or engineering report.

---

## Week of 2026-02-15

### 📄 Source
- **Title:** Mixture-of-Experts Meets Instruction Tuning: A Winning Combination for Large Language Models
- **Author(s) / Lab:** Shen et al. — Google DeepMind
- **Type:** arXiv paper
- **URL:** https://arxiv.org/abs/2305.14705
- **Published:** 2024-12-18

### 📝 Summary
This paper investigates the interaction between Mixture-of-Experts (MoE) architecture and instruction tuning for large language models. The authors demonstrate that MoE models benefit disproportionately from instruction tuning compared to dense counterparts — a finding with significant implications for cost-efficient model development. When instruction-tuned, a sparse MoE model with far fewer active parameters matches or exceeds the performance of dense models with 2–4× the compute budget. The paper provides ablation studies across model scales from 8B to 64B total parameters, showing consistent scaling behaviour. For practitioners, this confirms that MoE + instruction tuning is a viable strategy for deploying high-quality models under compute constraints. The results also suggest that expert specialization during instruction tuning leads to more efficient knowledge routing than during pretraining alone.

### 🔍 Key Engineering Insights
1. **Cost-performance tradeoff:** MoE models instruction-tuned on high-quality data can match dense models at 2–4× lower inference cost due to sparse activation — directly relevant for teams optimizing serving budgets on commodity GPUs.
2. **Expert routing matters post-tuning:** After instruction tuning, expert utilization becomes more balanced and specialized, reducing the "dead expert" problem common in naive MoE training. Monitor expert load balance metrics in production to detect routing degradation.
3. **Scaling strategy implication:** For organizations choosing between training a larger dense model or a larger-but-sparse MoE model, the paper provides evidence that MoE + instruction tuning yields better capability-per-FLOP, especially in the 8B–32B active parameter range that fits on single-node GPU deployments.

### 🏷️ Tags
`mixture-of-experts` `instruction-tuning` `llm-architecture`

---

## Week of 2026-02-22

### 📄 Source
- **Title:** From Local to Global: A Graph RAG Approach to Query-Focused Summarization
- **Author(s) / Lab:** Edge et al. — Microsoft Research
- **Type:** arXiv paper
- **URL:** https://arxiv.org/abs/2404.16130
- **Published:** 2025-01-15

### 📝 Summary
This paper introduces Graph RAG, a retrieval-augmented generation approach that constructs a knowledge graph from source documents and uses community detection to create hierarchical summaries for query-focused tasks. Unlike traditional RAG which retrieves individual chunks, Graph RAG first builds an entity-relationship graph from the entire corpus, applies the Leiden community detection algorithm to identify topical clusters, and then generates summaries at multiple levels of granularity. The approach significantly outperforms naive RAG on global sensemaking queries — questions that require synthesizing information across many documents rather than finding a single passage. Benchmarks on datasets ranging from podcast transcripts to scientific literature show 20–40% improvements in comprehensiveness and diversity of answers. The tradeoff is higher indexing cost: building the graph requires multiple LLM calls during the ingestion phase. For production systems handling analytical or exploratory queries over large corpora, Graph RAG offers a compelling alternative to chunk-based retrieval.

### 🔍 Key Engineering Insights
1. **When to use Graph RAG vs traditional RAG:** Graph RAG excels at "global" queries requiring synthesis across many documents (e.g., "What are the main themes?"), but traditional chunk-based RAG remains superior for "local" factoid queries (e.g., "What was the Q3 revenue?"). Design your retrieval strategy based on query distribution analysis.
2. **Indexing cost considerations:** The graph construction phase requires O(n) LLM calls where n is the number of text chunks — roughly 5–10× more expensive than embedding-only indexing. For a 10K document corpus, budget ~$15–30 in LLM API costs for initial graph construction, but subsequent queries are efficient.
3. **Community detection as chunking:** The Leiden algorithm's community hierarchy naturally produces multi-resolution summaries, eliminating the need for manual chunking strategy decisions. This is particularly valuable for heterogeneous corpora where fixed-size chunking performs poorly — but requires careful tuning of the resolution parameter to match query granularity.

### 🏷️ Tags
`rag` `knowledge-graphs` `query-focused-summarization`

---
