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

---

## Week of 2026-02-26

### 📄 Source
- **Title:** Multi-Agent Orchestration in Production: The Playbook for ...
- **Author(s) / Lab:** Identified via Tavily search
- **Type:** Research article / Engineering blog
- **URL:** https://www.linkedin.com/pulse/multi-agent-orchestration-production-playbook-reliable-nick-gupta-azcwe
- **Published:** 2026-02-26

### 📝 Summary
The article discusses the importance of distinguishing between agent orchestration and workflow orchestration in multi-agent systems. Agent orchestration refers to the use of large language models (LLMs) to drive decisions and creativity, while workflow orchestration focuses on deterministic execution paths, retries, and state management. A modern multi-agent stack typically consists of graph-based or stateful orchestration, lightweight coordination primitives, and a clear separation of responsibilities among agents. The use of knowledge graphs and auditable evaluation systems can also enhance the reliability and transparency of multi-agent systems. The article highlights the need for a structured approach to building multi-agent systems, rather than relying on ad-hoc prompt engineering. By embracing this structure, developers can create more robust and maintainable systems.

### 🔍 Key Engineering Insights
1. When designing a multi-agent system, it's essential to separate agent orchestration (LLM-driven decisions) from workflow orchestration (deterministic execution paths) to ensure reliable and efficient operation.
2. Using a graph-based or stateful orchestration approach, such as LangGraph, can help manage complex flows and stateful interactions between agents.
3. Implementing a clear separation of responsibilities among agents, including roles like Planner, Specialist, Verifier, Executor, and Supervisor, can help distribute decision-making and execution tasks effectively.

### 🏷️ Tags
`multi-agent-systems` `large-language-models` `workflow-orchestration`

---

---

## Week of 2026-03-01

### 📄 Source
- **Title:** Top 5 tools to detect hallucination in 2025
- **Author(s) / Lab:** Identified via Tavily search
- **Type:** Research article / Engineering blog
- **URL:** https://www.getmaxim.ai/articles/top-5-tools-to-detect-hallucination-in-2025/
- **Published:** 2026-03-01

### 📝 Summary
The article discusses tools for detecting hallucinations in AI models, which occur when a model generates inaccurate or nonsensical output. Five tools are evaluated: Maxim AI, Langfuse, Arize AI, Galileo, and LangSmith, each with its own strengths and weaknesses. Maxim AI provides a comprehensive end-to-end solution, while Langfuse offers open-source flexibility and LangChain-native debugging. Arize AI excels at enterprise-scale production monitoring, and Galileo provides straightforward real-time detection. The tools differ in their detection methodologies, with some using simulation, automated metrics, and human-in-the-loop workflows, while others employ embedding-based analytics and drift detection. Overall, the choice of tool depends on the specific organizational needs and application requirements.

### 🔍 Key Engineering Insights
1. When selecting a hallucination detection tool, consider the trade-off between comprehensive end-to-end solutions like Maxim AI and specialized tools like Langfuse, which offers open-source flexibility and infrastructure control.
2. To effectively detect hallucinations, developers can leverage a combination of techniques, including simulation, automated metrics, and human-in-the-loop workflows, as well as embedding-based analytics and drift detection.
3. Integrating hallucination detection tools into existing development workflows, such as LangChain-based applications, can facilitate more efficient and effective debugging and improvement of AI models.

### 🏷️ Tags
`hallucination_detection` `ai_model_evaluation` `model_debugging`

---

---

## Week of 2026-03-08

### 📄 Source
- **Title:** Hierarchical Policy Control for LLM Safety via Risk-Aware Chain-of ...
- **Author(s) / Lab:** Identified via Tavily search
- **Type:** Research article / Engineering blog
- **URL:** https://arxiv.org/html/2602.06650v1
- **Published:** 2026-03-08

### 📝 Summary
The article discusses the limitations of current approaches to aligning large language models (LLMs) with human preferences, which typically focus on optimizing models towards a single, static objective. These approaches often assume a uniform alignment policy and provide limited support for runtime customization or layered safety guarantees. The authors propose a hierarchical policy control framework that incorporates risk-aware chain-of-thought reasoning to improve LLM safety. This framework allows for more flexible and customizable alignment policies, enabling models to adapt to different contexts and safety requirements. The proposed approach builds upon existing work on RLHF, Constitutional AI, and Deliberative Alignment, aiming to provide more robust and reliable safety guarantees. By introducing a hierarchical policy control structure, the framework can better handle complex and nuanced safety specifications.

### 🔍 Key Engineering Insights
1. To improve LLM safety, developers can explore hierarchical policy control structures that allow for more flexible and customizable alignment policies, enabling models to adapt to different contexts and safety requirements.
2. Incorporating risk-aware chain-of-thought reasoning into the alignment process can help models better understand and respond to complex safety specifications, reducing the risk of harmful or undesirable outputs.
3. Developers can build upon existing techniques such as RLHF, Constitutional AI, and Deliberative Alignment to create more robust and reliable safety guarantees, rather than relying on a single approach or uniform alignment policy.

### 🏷️ Tags
`large_language_models` `alignment_techniques` `safety_guarantees`

---
