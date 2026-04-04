---
title: "Memory in the LLM Era: Modular Architectures and Strategies in a Unified Framework"
authors:
  - Yanchen Wu
  - Tenghui Lin
  - Yingli Zhou
  - Fangyuan Zhang
  - Qintian Guo
  - Xun Zhou
  - Sibo Wang
  - Xilin Liu
  - Yuchi Ma
  - Yixiang Fang
arxiv_id: "2604.01707"
arxiv_url: "https://arxiv.org/abs/2604.01707"
published: "2026-04-02"
updated: "2026-04-02"
source: "arXiv"
project: "memory"
scope_note: "pass-two meta include: survey/comparison"
agent_setting: "broad comparison across representative LLM memory methods and benchmarks"
memory_mechanism: "Meta paper that unifies existing memory methods into one modular framework and compares them under shared experimental settings."
icl_relevance: "medium"
tags:
  - agent-memory
  - survey
  - unified-framework
  - comparative-analysis
categories:
  - cs.CL
  - cs.DB
---

- **One-line take:** A comparative map of the field that is useful precisely because the mechanism literature is getting crowded and unevenly evaluated.
- **What it stores:** Not a single storage scheme; instead it analyzes modular combinations drawn from existing agent memory methods.
- **How memory is used at inference time:** Meta paper that unifies existing memory methods into one modular framework and compares them under shared experimental settings.
- **Why it matters for this sub-project:** Valuable for pass two because it helps contextualize the growing pile of mechanism papers and may prevent over-reading isolated benchmark wins.
- **Caveats / limits:** As a meta paper it depends on the choice of benchmarks and representative baselines, so its conclusions should guide judgment rather than settle it.
- **Abstract-level summary:** Memory emerges as the core module in the large language model (LLM)-based agents for long-horizon complex tasks (e.g., multi-turn dialogue, game playing, scientific discovery), where memory can enable knowledge accumulation, iterative reasoning and self-evolution. A number of memory methods have been proposed in the literature. However, these methods have not been systematically and comprehensively compared under the same experimental settings. In this paper, we first summarize a unified framework that incorporates all the existing agent memory methods from a high-level perspective. We then extensively compare representative agent memory methods on two well-known benchmarks and examine the effectiveness of all methods, providing a thorough analysis of those methods. As a byproduct of our experimental analysis, we also design a new memory method by exploiting modules in the existing methods, which outperforms the state-of-the-art methods. Finally, based on these findings, we offer promising future research opportunities. We believe that a deeper understanding of the behavior of existing methods can provide valuable new insights for future research.
