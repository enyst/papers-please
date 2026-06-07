---
title: "OEP: Poisoning Self-Evolving LLM Agents via Locally Correct but Non-Transferable Experiences"
authors:
  - Kaixiang Wang
  - Jiong Lou
  - Zhaojiacheng Zhou
  - Jie Li
arxiv_id: "2605.18930"
arxiv_url: "https://arxiv.org/abs/2605.18930"
published: "2026-05-18"
updated: "2026-05-18"
source: "arXiv"
project: "memory"
scope_note: "pass-four include (Q2 2026 sweep)"
agent_setting: "self-evolving LLM agents that consolidate reflections into reusable rules"
memory_mechanism: "Constructs adversarial edge-cases that are locally correct but non-transferable, biasing reflection toward over-generalized rules during consolidation."
icl_relevance: "medium"
tags:
  - agent-memory
  - security
  - memory-poisoning
  - self-evolving-agents
  - consolidation-attacks
categories:
  - cs.CR
  - cs.AI
  - cs.LG
---

- **One-line take:** Poisons the consolidation process itself — locally correct experiences become globally harmful rules.
- **What it stores:** See memory_mechanism above.
- **How memory is used at inference time:** Constructs adversarial edge-cases that are locally correct but non-transferable, biasing reflection toward over-generalized rules during consolidation.
- **Why it matters for this sub-project:** Shows that consolidation — which we treat as a defense point — can itself be an attack surface.
- **Caveats / limits:** Newly published (Q2 2026); peer validation pending.
- **Abstract-level summary:** Memory-augmented large language model (LLM) agents use iterative reflection and self-evolution to solve complex tasks, but these mechanisms introduce security risks. Existing agentic memory attacks require privileged access or explicit malicious content, making them detectable by advanced safety filters. This leaves a subtler attack surface underexplored: whether adversaries can induce agent to generate experiences that appear locally correct and semantically plausible yet induce harmful generalization during reflection. We find that reflective agents are vulnerable to such clean experiences, especially when paired with severe but plausible hypothetical consequences. Based on this observation, we introduce Obsessive Experience Poisoning (OEP), a low-privilege black-box attack requiring no direct control over the system prompt or memory database. OEP constructs adversarial clean edge-cases that combine locally correct solutions, non-transferable methods, and severe consequences, biasing reflection toward risk-averse rule formation. During memory consolidation, agents may over-trust self-generated reflections and distill localized experiences into high-priority but over-generalized rules, causing downstream failures. Evaluations across three domains show that OEP achieves ASR above 50\% with GPT-4o agents, and outperforms existing attacks under LLM auditing defense.
