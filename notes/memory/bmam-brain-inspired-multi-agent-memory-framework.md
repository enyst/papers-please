---
title: "BMAM: Brain-inspired Multi-Agent Memory Framework"
authors:
  - Yang Li
  - Jiaxiang Liu
  - Yusong Wang
  - Yujie Wu
  - Mingkun Xu
arxiv_id: "2601.20465"
arxiv_url: "https://arxiv.org/abs/2601.20465"
published: "2026-01-28"
updated: "2026-01-28"
source: "arXiv"
project: "memory"
scope_note: "core include"
agent_setting: "long-horizon conversational agents"
memory_mechanism: "Splits memory into specialized subsystems such as episodic, semantic, salience-aware, and control-oriented memory with explicit timelines."
icl_relevance: "medium"
tags:
  - agent-memory
  - episodic-memory
  - semantic-memory
  - long-horizon-dialogue
categories:
  - cs.CL
---

- **One-line take:** Shows the value of decomposing memory by function and timescale instead of keeping one undifferentiated store.
- **What it stores:** Temporally grounded episodes plus semantic and control-oriented summaries.
- **How memory is used at inference time:** Splits memory into specialized subsystems such as episodic, semantic, salience-aware, and control-oriented memory with explicit timelines.
- **Why it matters for this sub-project:** Helpful when thinking about memory architecture at the system level, especially for temporal reasoning over long interaction histories.
- **Caveats / limits:** More of an architectural decomposition than a minimal recipe, and most evidence comes from benchmark-style long conversation tasks.
- **Abstract-level summary:** Language-model-based agents operating over extended interaction horizons face persistent challenges in preserving temporally grounded information and maintaining behavioral consistency across sessions, a failure mode we term soul erosion. We present BMAM (Brain-inspired Multi-Agent Memory), a general-purpose memory architecture that models agent memory as a set of functionally specialized subsystems rather than a single unstructured store. Inspired by cognitive memory systems, BMAM decomposes memory into episodic, semantic, salience-aware, and control-oriented components that operate at complementary time scales. To support long-horizon reasoning, BMAM organizes episodic memories along explicit timelines and retrieves evidence by fusing multiple complementary signals. Experiments on the LoCoMo benchmark show that BMAM achieves 78.45 percent accuracy under the standard long-horizon evaluation setting, and ablation analyses confirm that the hippocampus-inspired episodic memory subsystem plays a critical role in temporal reasoning.
