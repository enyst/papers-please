---
title: "MemGym: a Long-Horizon Memory Environment for LLM Agents"
authors:
  - Wujiang Xu
  - Yu Wang
  - Kai Mei
  - Kaiqu Liang
  - Zhenting Wang
  - Mingyu Jin
  - Han Zhang
  - Shi-Xiong Zhang
  - Wenyue Hua
  - Sambit Sahu
  - Dimitris N. Metaxas
arxiv_id: "2605.20833"
arxiv_url: "https://arxiv.org/abs/2605.20833"
published: "2026-05-20"
updated: "2026-05-20"
source: "arXiv"
project: "memory"
scope_note: "pass-four include (Q2 2026 sweep)"
agent_setting: "long-horizon memory evaluation for LLM agents"
memory_mechanism: "An environment-based benchmark that tests dynamic memory formation during extended agent execution, not just recall of stored facts."
icl_relevance: "medium"
tags:
  - agent-memory
  - benchmark
  - long-horizon
  - evaluation
categories:
  - cs.CL
---

- **One-line take:** Tests memory as it forms during execution, not just recall of pre-stored facts — a more realistic evaluation.
- **What it stores:** See memory_mechanism above.
- **How memory is used at inference time:** An environment-based benchmark that tests dynamic memory formation during extended agent execution, not just recall of stored facts.
- **Why it matters for this sub-project:** Fills a gap: most benchmarks test retrieval, this one tests the full memory lifecycle during real task execution.
- **Caveats / limits:** Newly published (Q2 2026); peer validation pending.
- **Abstract-level summary:** Memory is a central capability for LLM agents operating across long-horizon tasks. Existing memory benchmarks predominantly evaluate retention of personalized information in multi-turn chat scenarios, overlooking the dynamic memory formation that occurs during extended agent execution. Consequently, the memory systems they produce transfer poorly to realistic agentic environments, such as coding and web navigation. We present MemGym, a benchmark for agentic memory that unifies existing agent gyms and in-house memory-grounded pipelines behind one memory-reasoning interface. MemGym spans five evaluation tracks grouped into four agentic regimes: tool-use dialogue (tau2-bench), multi-turn deep-research search (MEMGYM-DR), coding (SWE-Gym and MEMGYM-CODEQA), and computer use (WebArena-Infinity). MemGym reports memory-isolated scores that decouple memory performance from reasoning, retrieval, and tool-use ability, so memory strategies can be ranked without those confounders. Our synthetic pipelines for MEMGYM-CODEQA and MEMGYM-DR are length-controllable, ablation-verified at every stage, and tightly aligned with downstream scenarios. To make evaluation on coding environments academically tractable, we train MemRM, a lightweight reward model (Qwen3-1.7B fine-tuned with QLoRA) that scores compression quality as a fast scalar read in place of full Docker rollouts.
