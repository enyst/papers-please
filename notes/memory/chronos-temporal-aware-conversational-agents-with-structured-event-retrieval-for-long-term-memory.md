---
title: "Chronos: Temporal-Aware Conversational Agents with Structured Event Retrieval for Long-Term Memory"
authors:
  - Sahil Sen
  - Elias Lumer
  - Anmol Gulati
  - Vamse Kumar Subbiah
arxiv_id: "2603.16862"
arxiv_url: "https://arxiv.org/abs/2603.16862"
published: "2026-03-17"
updated: "2026-03-17"
source: "arXiv"
project: "memory"
scope_note: "core include"
agent_setting: "conversational agents that must answer temporally grounded long-term queries"
memory_mechanism: "Builds structured event and turn calendars, then uses dynamic prompting plus iterative tool calls to retrieve temporally relevant memory."
icl_relevance: "high"
tags:
  - agent-memory
  - temporal-memory
  - event-retrieval
  - conversation-memory
categories:
  - cs.CL
---

- **One-line take:** A strong temporal-memory design for the cases where “what happened when” matters as much as “what happened”.
- **What it stores:** Structured subject-verb-object events with datetime ranges, entity aliases, and turn-level conversational context.
- **How memory is used at inference time:** Builds structured event and turn calendars, then uses dynamic prompting plus iterative tool calls to retrieve temporally relevant memory.
- **Why it matters for this sub-project:** Important for pass two because temporal reasoning remains one of the main weak spots of long-term conversation memory systems.
- **Caveats / limits:** The structured calendar representation is powerful but specialized; it may not generalize equally well to non-conversational or non-temporal agent settings.
- **Abstract-level summary:** Recent advances in Large Language Models (LLMs) have enabled conversational AI agents to engage in extended multi-turn interactions spanning weeks or months. However, existing memory systems struggle to reason over temporally grounded facts and preferences that evolve across months of interaction and lack effective retrieval strategies for multi-hop, time-sensitive queries over long dialogue histories. We introduce Chronos, a novel temporal-aware memory framework that decomposes raw dialogue into subject-verb-object event tuples with resolved datetime ranges and entity aliases, indexing them in a structured event calendar alongside a turn calendar that preserves full conversational context. At query time, Chronos applies dynamic prompting to generate tailored retrieval guidance for each question, directing the agent on what to retrieve, how to filter across time ranges, and how to approach multi-hop reasoning through an iterative tool-calling loop over both calendars. We evaluate Chronos with 8 LLMs, both open-source and closed-source, on the LongMemEvalS benchmark comprising 500 questions spanning six categories of dialogue history tasks. Chronos Low achieves 92.60% and Chronos High scores 95.60% accuracy, setting a new state of the art with an improvement of 7.67% over the best prior system. Ablation results reveal the events calendar accounts for a 58.9% gain on the baseline while all other components yield improvements between 15.5% and 22.3%. Notably, Chronos Low alone surpasses prior approaches evaluated under their strongest model configurations.
