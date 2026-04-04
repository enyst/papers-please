---
title: "HyMem: Hybrid Memory Architecture with Dynamic Retrieval Scheduling"
authors:
  - Xiaochen Zhao
  - Kaikai Wang
  - Xiaowen Zhang
  - Chen Yao
  - Aili Wang
arxiv_id: "2602.13933"
arxiv_url: "https://arxiv.org/abs/2602.13933"
published: "2026-02-15"
updated: "2026-02-15"
source: "arXiv"
project: "memory"
scope_note: "core include"
agent_setting: "LLM agents in extended dialogues where memory cost and reasoning depth must be balanced"
memory_mechanism: "Combines summary-level and deep memory modules with dynamic two-tier retrieval so expensive deep reasoning is invoked only when needed."
icl_relevance: "high"
tags:
  - agent-memory
  - hybrid-memory
  - dynamic-retrieval
  - efficiency
categories:
  - cs.AI
---

- **One-line take:** A flexible memory scheduler that tries to pay for deep retrieval only on genuinely hard queries.
- **What it stores:** Multi-granular memory representations spanning lightweight summaries and richer detail-level context.
- **How memory is used at inference time:** Combines summary-level and deep memory modules with dynamic two-tier retrieval so expensive deep reasoning is invoked only when needed.
- **Why it matters for this sub-project:** Useful because it sharpens the efficiency-vs-recall tradeoff that many persistent-memory systems struggle with.
- **Caveats / limits:** Its benefits depend on correctly deciding when a query warrants the deeper retrieval path.
- **Abstract-level summary:** Large language model (LLM) agents demonstrate strong performance in short-text contexts but often underperform in extended dialogues due to inefficient memory management. Existing approaches face a fundamental trade-off between efficiency and effectiveness: memory compression risks losing critical details required for complex reasoning, while retaining raw text introduces unnecessary computational overhead for simple queries. The crux lies in the limitations of monolithic memory representations and static retrieval mechanisms, which fail to emulate the flexible and proactive memory scheduling capabilities observed in humans, thus struggling to adapt to diverse problem scenarios. Inspired by the principle of cognitive economy, we propose HyMem, a hybrid memory architecture that enables dynamic on-demand scheduling through multi-granular memory representations. HyMem adopts a dual-granular storage scheme paired with a dynamic two-tier retrieval system: a lightweight module constructs summary-level context for efficient response generation, while an LLM-based deep module is selectively activated only for complex queries, augmented by a reflection mechanism for iterative reasoning refinement. Experiments show that HyMem achieves strong performance on both the LOCOMO and LongMemEval benchmarks, outperforming full-context while reducing computational cost by 92.6\%, establishing a state-of-the-art balance between efficiency and performance in long-term memory management.
