---
title: "UMEM: Unified Memory Extraction and Management Framework for Generalizable Memory"
authors:
  - Yongshi Ye
  - Hui Jiang
  - Feihu Jiang
  - Tian Lan
  - Yichao Du
  - Biao Fu
  - Xiaodong Shi
  - Qianghuai Jia
  - Longyue Wang
  - Weihua Luo
arxiv_id: "2602.10652"
arxiv_url: "https://arxiv.org/abs/2602.10652"
published: "2026-02-11"
updated: "2026-02-11"
source: "arXiv"
project: "memory"
scope_note: "borderline include: it targets deployed memory, but the paper uses learning to optimize the extractor/manager."
agent_setting: "self-evolving LLM agents that continuously build memory from experience"
memory_mechanism: "Jointly optimizes memory extraction and memory-bank updates so the agent keeps more generalizable memories rather than instance-specific noise."
icl_relevance: "medium"
tags:
  - agent-memory
  - memory-extraction
  - memory-management
  - borderline-trained
categories:
  - cs.CL
---

- **One-line take:** Addresses an overlooked point: bad memory often starts at extraction time, not only at retrieval time.
- **What it stores:** Generalizable memories distilled from semantically related experiences rather than isolated instances.
- **How memory is used at inference time:** Jointly optimizes memory extraction and memory-bank updates so the agent keeps more generalizable memories rather than instance-specific noise.
- **Why it matters for this sub-project:** Conceptually valuable because it treats extraction and management as one loop instead of two disconnected stages.
- **Caveats / limits:** Borderline for this corpus because the method leans on learned optimization rather than a purely inference-time memory mechanism.
- **Abstract-level summary:** Self-evolving memory serves as the trainable parameters for Large Language Models (LLMs)-based agents, where extraction (distilling insights from experience) and management (updating the memory bank) must be tightly coordinated. Existing methods predominately optimize memory management while treating memory extraction as a static process, resulting in poor generalization, where agents accumulate instance-specific noise rather than robust memories. To address this, we propose Unified Memory Extraction and Management (UMEM), a self-evolving agent framework that jointly optimizes a Large Language Model to simultaneous extract and manage memories. To mitigate overfitting to specific instances, we introduce Semantic Neighborhood Modeling and optimize the model with a neighborhood-level marginal utility reward via GRPO. This approach ensures memory generalizability by evaluating memory utility across clusters of semantically related queries. Extensive experiments across five benchmarks demonstrate that UMEM significantly outperforms highly competitive baselines, achieving up to a 10.67% improvement in multi-turn interactive tasks. Futhermore, UMEM maintains a monotonic growth curve during continuous evolution. Codes and models will be publicly released.
