---
title: "Where Code Meets Natural Language: Taxonomy-Driven Information Flow Analysis for LLM-Integrated Applications"
authors:
  - Zihao Xu
  - Xiao Cheng
  - Ruijie Meng
  - Yuekang Li
arxiv_id: "2603.28345"
arxiv_url: "https://arxiv.org/abs/2603.28345"
published: "2026-03-30"
updated: "2026-05-26"
source: "arXiv"
project: "prompt-injection"
scope_note: "initial sweep"
agent_setting: "LLM agents with tool use and/or persistent state"
defense_approach: "information-flow"
defense_type: "Taxonomy-driven information flow analysis across the LLM boundary"
tags:
  - prompt-injection
  - defense
  - information-flow
  - taint-tracking
  - program-analysis
categories:
  - cs.SE
  - cs.AI
---

- **One-line take:** Treat the LLM as a program boundary and apply information flow analysis — taint tracking for prompts.
- **Defense approach:** Taxonomy-driven information flow analysis across the LLM boundary
- **Pros:** Principled (borrows from PL security); can be automated; catches flows traditional analysis misses
- **Cons:** Requires program analysis tooling; LLM is opaque; early-stage research
- **Abstract-level summary:** LLM API calls are becoming a ubiquitous program construct, yet they create a boundary that no existing program analysis can cross: runtime values enter a natural-language prompt, undergo opaque processing inside the LLM, and re-emerge as code, SQL, JSON, or text that the program consumes. Every analysis that tracks data across function boundaries, including taint analysis, program slicing, dependency analysis, and change-impact analysis, relies on dataflow summaries of callee behavior. LLM calls have no such summaries, breaking all of these analyses at what we call the NL/PL boundary.   We pre
