---
title: "What If Prompt Injection Never Left? Exploring Cross-Session Stored Prompt Injection in Agentic Systems"
authors:
  - Yuanbo Xie
  - Tianyun Liu
  - Yingjie Zhang
  - Suchen Liu
  - Yulin Li
  - Liya Su
  - Tingwen Liu
arxiv_id: "2606.04425"
arxiv_url: "https://arxiv.org/abs/2606.04425"
published: "2026-06-03"
updated: "2026-06-03"
source: "arXiv"
project: "prompt-injection"
scope_note: "initial sweep"
agent_setting: "LLM agents with tool use and/or persistent state"
defense_approach: "cross-session-injection"
defense_type: "Analysis of how injections persist across sessions via stored state"
tags:
  - prompt-injection
  - cross-session
  - stored-injection
  - agentic-systems
  - persistence
categories:
  - cs.CR
  - cs.AI
---

- **One-line take:** Prompt injection never left — it just moved into the agent's memory, filesystem, and tool outputs.
- **Defense approach:** Analysis of how injections persist across sessions via stored state
- **Pros:** Identifies the full lifecycle of stored injections; practical focus on agentic systems
- **Cons:** Diagnosis-heavy; defenses are directions, not solutions
- **Abstract-level summary:** Modern agentic systems transform LLMs from session-bounded assistants into stateful systems that persist and evolve shared world state across sessions through memories, filesystems, tools, and other long-lived contextual artifacts. This shift fundamentally expands the attack surface of prompt injection. However, prior works on prompt injection have largely focused on model-level threats within a single session, overlooking how cross-session persistent system state fundamentally changes the system-level risk of agentic systems. Inspired by stored cross-site scripting in web systems, we introduc
