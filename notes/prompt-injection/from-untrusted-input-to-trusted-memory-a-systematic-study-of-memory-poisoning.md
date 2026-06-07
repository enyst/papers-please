---
title: "From Untrusted Input to Trusted Memory: A Systematic Study of Memory Poisoning Attacks in LLM Agents"
authors:
  - Pritam Dash
  - Tongyu Ge
  - Aditi Jain
  - Tanmay Shah
  - Zhiwei Shang
arxiv_id: "2606.04329"
arxiv_url: "https://arxiv.org/abs/2606.04329"
published: "2026-06-03"
updated: "2026-06-03"
source: "arXiv"
project: "prompt-injection"
scope_note: "initial sweep"
agent_setting: "LLM agents with tool use and/or persistent state"
defense_approach: "memory-poisoning"
defense_type: "Systematic study of how prompt injection persists through memory systems"
tags:
  - prompt-injection
  - memory-poisoning
  - persistence
  - cross-session
  - agent-memory
categories:
  - cs.CR
  - cs.AI
---

- **One-line take:** Prompt injection meets persistent memory — the injection outlives the session.
- **Defense approach:** Systematic study of how prompt injection persists through memory systems
- **Pros:** Critical framing: injection + memory = persistent compromise; systematic threat model
- **Cons:** More diagnosis than cure; defense proposals are preliminary
- **Abstract-level summary:** Memory is a core component of AI agents, enabling them to accumulate knowledge across interactions and improve performance. However, persistent memory introduces the risk of memory poisoning, where a single adversarial memory write can exert long-term influence over agent behavior. We present a systematic study of memory poisoning in LLM-based agents. We identify four memory write channels and nine structural vulnerabilities in model capabilities, system prompt design, and agent system architecture that make these channels exploitable. Based on these vulnerabilities, we develop a taxonomy of s
