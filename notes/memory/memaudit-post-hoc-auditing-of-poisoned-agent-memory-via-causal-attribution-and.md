---
title: "MemAudit: Post-hoc Auditing of Poisoned Agent Memory via Causal Attribution and Structural Anomaly Detection"
authors:
  - Zhewen Tan
  - Yilun Yao
  - Huiyan Jin
  - Wenhan Yu
  - Guoan Wang
  - Mengyuan Fan
  - liang lu
  - Feng Liu
  - Xiangzheng Zhang
  - Duohe Ma
  - Tong Yang
  - Lin Sun
arxiv_id: "2605.23723"
arxiv_url: "https://arxiv.org/abs/2605.23723"
published: "2026-05-22"
updated: "2026-05-22"
source: "arXiv"
project: "memory"
scope_note: "pass-four include (Q2 2026 sweep)"
agent_setting: "post-hoc auditing of poisoned agent memory stores"
memory_mechanism: "Uses causal attribution and structural anomaly detection to identify poisoned entries in existing memory stores."
icl_relevance: "medium"
tags:
  - agent-memory
  - security
  - memory-auditing
  - causal-attribution
categories:
  - cs.AI
---

- **One-line take:** Detect-after-the-fact: audit your memory store for poisoning without needing to prevent it at write time.
- **What it stores:** See memory_mechanism above.
- **How memory is used at inference time:** Uses causal attribution and structural anomaly detection to identify poisoned entries in existing memory stores.
- **Why it matters for this sub-project:** Complements prevention-focused defenses (AgentSys, MemLineage) with a detection-focused approach.
- **Caveats / limits:** Newly published (Q2 2026); peer validation pending.
- **Abstract-level summary:** Large language model agents increasingly rely on persistent memory to store past interactions, retrieve relevant demonstrations, and improve long-horizon task execution. However, this memory mechanism also creates a practical security vulnerability: an adversarial user may inject malicious records into the agent's memory through ordinary interaction, and these records can later be retrieved to steer the agent's reasoning and actions. Existing defenses primarily focus on online intervention, such as prompt filtering or output blocking, but they do not address the post-hoc question of which stored memories are responsible after harmful behavior has already been observed. We propose \textbf{MemAudit}, a post-hoc causal memory auditing framework for memory-augmented LLM agents. The framework combines two complementary signals: (1) a counterfactual memory influence score that measures each memory's causal contribution to harmful outputs, and (2) a memory consistency graph that identifies structurally anomalous memories within the broader memory store. We evaluate MemAudit against MINJA, a query-only memory injection attack in which malicious records are generated and stored through normal agent interactions rather than direct memory-bank modification. Across both QA and reasoning-agent settings, MemAudit substantially reduces attack success rates under realistic post-hoc auditing scenarios. The results show that QA attack success is reduced from $70\%$ to $0\%$, while RAP attack success drops from $83.3\%$ to $0\%$.
