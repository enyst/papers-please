---
title: "Hierarchical Memory Orchestration for Personalized Persistent Agents"
authors:
  - Junming Liu
  - Yifei Sun
  - Weihua Cheng
  - Haodong Lei
  - Yuqi Li
  - Yirong Chen
  - Ding Wang
arxiv_id: "2604.01670"
arxiv_url: "https://arxiv.org/abs/2604.01670"
published: "2026-04-02"
updated: "2026-04-02"
source: "arXiv"
project: "memory"
scope_note: "core include"
agent_setting: "persistent personalized agents, including edge/device-constrained deployments"
memory_mechanism: "Organizes interaction history into active, secondary, and archival tiers guided by evolving user persona and contextual relevance."
icl_relevance: "high"
tags:
  - agent-memory
  - hierarchical-memory
  - personalization
  - persistent-agents
categories:
  - cs.AI
---

- **One-line take:** A strong example of memory orchestration for personalization: keep the active set lean while preserving a full archive underneath.
- **What it stores:** Recent and pivotal memories, an evolving user profile, and a larger archive of historical interactions.
- **How memory is used at inference time:** Organizes interaction history into active, secondary, and archival tiers guided by evolving user persona and contextual relevance.
- **Why it matters for this sub-project:** Useful for persistent assistants where latency and personalization compete directly for context budget.
- **Caveats / limits:** The setting is personalized-assistant heavy, so the recipe may need adaptation for broader non-personal agent workflows.
- **Abstract-level summary:** While long-term memory is essential for intelligent agents to maintain consistent historical awareness, the accumulation of extensive interaction data often leads to performance bottlenecks. Naive storage expansion increases retrieval noise and computational latency, overwhelming the reasoning capacity of models deployed on constrained personal devices. To address this, we propose Hierarchical Memory Orchestration (HMO), a framework that organizes interaction history into a three-tiered directory driven by user-centric contextual relevance. Our system maintains a compact primary cache, coupling recent and pivotal memories with an evolving user profile to ensure agent reasoning remains aligned with individual behavioral traits. This primary cache is complemented by a high-priority secondary layer, both of which are managed within a global archive of the full interaction history. Crucially, the user persona dictates memory redistribution across this hierarchy, promoting records mapped to long-term patterns toward more active tiers while relegating less relevant information. This targeted orchestration surfaces historical knowledge precisely when needed while maintaining a lean and efficient active search space. Evaluations on multiple benchmarks achieve state-of-the-art performance. Real-world deployments in ecosystems like OpenClaw demonstrate that HMO significantly enhances agent fluidity and personalization.
