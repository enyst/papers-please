---
title: "ER-MIA: Black-Box Adversarial Memory Injection Attacks on Long-Term Memory-Augmented Large Language Models"
authors:
  - Mitchell Piehl
  - Zhaohan Xi
  - Zuobin Xiong
  - Pan He
  - Muchao Ye
arxiv_id: "2602.15344"
arxiv_url: "https://arxiv.org/abs/2602.15344"
published: "2026-02-17"
updated: "2026-02-17"
source: "arXiv"
project: "memory"
scope_note: "pass-two security include"
agent_setting: "long-term memory-augmented LLM systems using similarity-based retrieval"
memory_mechanism: "Analyzes black-box attacks that inject adversarial memory entries to manipulate later retrieval and downstream behavior."
icl_relevance: "medium"
tags:
  - agent-memory
  - security
  - memory-injection
  - retrieval-attacks
categories:
  - cs.LG
---

- **One-line take:** Shows that similarity-based memory retrieval is a system-level security weakness, not just a modeling choice.
- **What it stores:** Long-term memory entries that can be adversarially crafted to dominate retrieval under realistic assumptions.
- **How memory is used at inference time:** Analyzes black-box attacks that inject adversarial memory entries to manipulate later retrieval and downstream behavior.
- **Why it matters for this sub-project:** Important for pass two because it pressure-tests many retrieval-centric memory papers in the corpus and highlights where their assumptions may break under attack.
- **Caveats / limits:** Security analysis does not automatically translate into a better memory mechanism; the main contribution is exposing risk rather than resolving it.
- **Abstract-level summary:** Large language models (LLMs) are increasingly augmented with long-term memory systems to overcome finite context windows and enable persistent reasoning across interactions. However, recent research finds that LLMs become more vulnerable because memory provides extra attack surfaces. In this paper, we present the first systematic study of black-box adversarial memory injection attacks that target the similarity-based retrieval mechanism in long-term memory-augmented LLMs. We introduce ER-MIA, a unified framework that exposes this vulnerability and formalizes two realistic attack settings: content-based attacks and question-targeted attacks. In these settings, ER-MIA includes an arsenal of composable attack primitives and ensemble attacks that achieve high success rates under minimal attacker assumptions. Extensive experiments across multiple LLMs and long-term memory systems demonstrate that similarity-based retrieval constitutes a fundamental and system-level vulnerability, revealing security risks that persist across memory designs and application scenarios.
