---
title: "MemBuilder: Reinforcing LLMs for Long-Term Memory Construction via Attributed Dense Rewards"
authors:
  - Zhiyu Shen
  - Ziming Wu
  - Fuming Lai
  - Shaobing Lian
  - Yanghui Rao
arxiv_id: "2601.05488"
arxiv_url: "https://arxiv.org/abs/2601.05488"
published: "2026-01-09"
updated: "2026-02-02"
source: "arXiv"
project: "memory"
scope_note: "pass-three borderline include: training-heavy memory construction"
agent_setting: "long-term dialogue agents that need consistent memory construction over extended sessions"
memory_mechanism: "Uses reinforcement learning with dense rewards to train a model to orchestrate multi-dimensional memory construction across dialogue trajectories."
icl_relevance: "medium"
tags:
  - agent-memory
  - long-term-dialogue
  - memory-construction
  - borderline-trained
categories:
  - cs.CL
---

- **One-line take:** Treats memory construction itself as a trainable policy rather than a fixed prompting pipeline.
- **What it stores:** Multi-dimensional dialogue memories whose components are attributed and rewarded based on downstream usefulness.
- **How memory is used at inference time:** Uses reinforcement learning with dense rewards to train a model to orchestrate multi-dimensional memory construction across dialogue trajectories.
- **Why it matters for this sub-project:** Worth keeping because it shows where the literature is going when inference-time memory design starts blending into learned memory-management policies.
- **Caveats / limits:** Borderline for this corpus because the core contribution is RL training, not a purely deployment-time memory mechanism.
- **Abstract-level summary:** Maintaining consistency in long-term dialogues remains a fundamental challenge for LLMs, as standard retrieval mechanisms often fail to capture the temporal evolution of historical states. While memory-augmented frameworks offer a structured alternative, current systems rely on static prompting of closed-source models or suffer from ineffective training paradigms with sparse rewards. We introduce MemBuilder, a reinforcement learning framework that trains models to orchestrate multi-dimensional memory construction with attributed dense rewards. MemBuilder addresses two key challenges: (1) Sparse Trajectory-Level Rewards: we employ synthetic session-level question generation to provide dense intermediate rewards across extended trajectories; and (2) Multi-Dimensional Memory Attribution: we introduce contribution-aware gradient weighting that scales policy updates based on each component's downstream impact. Experimental results show that MemBuilder enables a 4B-parameter model to outperform state-of-the-art closed-source baselines, exhibiting strong generalization across long-term dialogue benchmarks.
