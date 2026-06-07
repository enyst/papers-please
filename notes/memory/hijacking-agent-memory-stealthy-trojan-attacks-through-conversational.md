---
title: "Hijacking Agent Memory: Stealthy Trojan Attacks Through Conversational Interaction"
authors:
  - Hongtao Wang
  - Se Yang
  - Yu Chen
  - Puzhuo Liu
arxiv_id: "2605.29960"
arxiv_url: "https://arxiv.org/abs/2605.29960"
published: "2026-05-28"
updated: "2026-05-28"
source: "arXiv"
project: "memory"
scope_note: "pass-four include (Q2 2026 sweep)"
agent_setting: "LLM agents with long-term conversational memory"
memory_mechanism: "Bypasses selective memory extraction via semantic relational bridges, entity masquerading, and joint embedding optimization to inject trojans through dialogue."
icl_relevance: "medium"
tags:
  - agent-memory
  - security
  - memory-poisoning
  - trojan-attacks
categories:
  - cs.CR
  - cs.AI
---

- **One-line take:** A stealthy attack that defeats modern selective memory pipelines — 0.95 ASR against real extraction mechanisms.
- **What it stores:** See memory_mechanism above.
- **How memory is used at inference time:** Bypasses selective memory extraction via semantic relational bridges, entity masquerading, and joint embedding optimization to inject trojans through dialogue.
- **Why it matters for this sub-project:** Shows that selective extraction is not a sufficient defense — attacks can be crafted to survive modern memory pipelines.
- **Caveats / limits:** Newly published (Q2 2026); peer validation pending.
- **Abstract-level summary:** Large language model (LLM) agents increasingly leverage long term memory to support persistent and autonomous task execution. However, this capability also introduces a new attack surface: memory poisoning, where adversaries can inject malicious information to influence future behavior. Existing memory poisoning attacks often assume that injected content can be stored directly in memory, overlooking the selective extraction and rewriting stages in modern memory pipelines. This makes prior methods ineffective under realistic settings.   In this paper, we propose MemPoison, a novel memory poisoning attack that bypasses selective memory mechanisms in LLM agents, where an attacker can inject triggerable backdoors into the agent's long-term memory through dialogue interactions, thereby misleading its subsequent responses. MemPoison introduces three key components: (i) a semantic relational bridge that binds the trigger and payload into a coherent statement to ensure they are extracted into memory together; (ii) entity masquerading that optimizes triggers to mimic named entities, resisting rewriting; and (iii) joint embedding optimization that shapes trigger-injected texts into a tight cluster in the embedding space while maintaining isolation from benign embeddings for stealth. Evaluations across different agent domains and memory mechanisms show MemPoison achieves attack success rates up to 0.95, outperforming existing baselines. Mechanistic analysis indicates that the attack exploits embedding-space anisotropy and shifts attention patterns, highlighting core vulnerabilities in selective memory systems. We evaluate multiple defense strategies and demonstrate their fundamental limitations in mitigating the attack.
