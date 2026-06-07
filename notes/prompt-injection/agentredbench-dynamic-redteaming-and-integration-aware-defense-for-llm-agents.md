---
title: "AgentRedBench: Dynamic Redteaming and Integration-Aware Defense for LLM Agents over SaaS Integrations"
authors:
  - Hiskias Dingeto
  - William Leeney
arxiv_id: "2606.02240"
arxiv_url: "https://arxiv.org/abs/2606.02240"
published: "2026-06-01"
updated: "2026-06-02"
source: "arXiv"
project: "prompt-injection"
scope_note: "initial sweep"
agent_setting: "LLM agents with tool use and/or persistent state"
defense_approach: "redteam-and-defend"
defense_type: "Dynamic red-teaming with integration-aware defense for SaaS tool-use agents"
tags:
  - prompt-injection
  - defense
  - red-teaming
  - saas-integration
  - tool-use
categories:
  - cs.CR
  - cs.AI
  - cs.CL
  - cs.ET
---

- **One-line take:** Red-team the agent in its actual tool environment, then build defenses that know the integration context.
- **Defense approach:** Dynamic red-teaming with integration-aware defense for SaaS tool-use agents
- **Pros:** Realistic threat model (actual SaaS tools); integration-aware; dynamic, not static rules
- **Cons:** Expensive to run; SaaS-specific; may not cover novel tool combinations
- **Abstract-level summary:** Indirect prompt injection in tool-use agents is a concrete production threat: LLM agents read from integrations (third-party services such as Gmail, Salesforce, or Jira accessed through tool calls) whose response content the user neither writes nor controls. Existing benchmarks under-measure the threat: most cover only a handful of integrations with the same attack payload replayed across runs, and open-source guards are trained on chat-style data rather than tool-response content. We introduce AGENTREDBENCH, a dynamic LLM-driven redteaming benchmark of 215 subtle underspecified authorization 
