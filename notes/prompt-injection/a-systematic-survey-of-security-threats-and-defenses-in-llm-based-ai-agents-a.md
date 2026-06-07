---
title: "A Systematic Survey of Security Threats and Defenses in LLM-Based AI Agents: A Layered Attack Surface Framework"
authors:
  - Kexin Chu
arxiv_id: "2604.23338"
arxiv_url: "https://arxiv.org/abs/2604.23338"
published: "2026-04-25"
updated: "2026-05-06"
source: "arXiv"
project: "prompt-injection"
scope_note: "initial sweep"
agent_setting: "LLM agents with tool use and/or persistent state"
defense_approach: "survey"
defense_type: "Survey/taxonomy of the full threat and defense landscape"
tags:
  - prompt-injection
  - survey
  - taxonomy
  - agent-security
  - attack-surface
categories:
  - cs.CR
  - cs.LG
---

- **One-line take:** The most comprehensive survey — maps attacks and defenses across a layered agent attack surface framework.
- **Defense approach:** Survey/taxonomy of the full threat and defense landscape
- **Pros:** Comprehensive coverage; useful mental model (layered framework); covers memory, tools, multi-agent, cross-session
- **Cons:** Survey, not a defense mechanism itself; broad but not deep on any single approach
- **Abstract-level summary:** Agentic AI systems introduce a security surface that is qualitatively different from that of stateless LLMs. They persist memory, invoke external tools, coordinate with peer agents, and operate across sessions, allowing attacks to emerge not only at the prompt interface but also through architectural state, delegated authority, and long-horizon interactions. Existing security taxonomies, however, primarily organize threats by attack type, such as prompt injection or jailbreaking, and therefore obscure where in the agentic stack a threat arises and over what timescale it manifests.   We propose
