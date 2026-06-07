---
title: "AgentVisor: Defending LLM Agents Against Prompt Injection via Semantic Virtualization"
authors:
  - Zonghao Ying
  - Haozheng Wang
  - Jiangfan Liu
  - Quanchen Zou
  - Aishan Liu
  - Jian Yang
  - Yaodong Yang
  - Xianglong Liu
arxiv_id: "2604.24118"
arxiv_url: "https://arxiv.org/abs/2604.24118"
published: "2026-04-27"
updated: "2026-04-27"
source: "arXiv"
project: "prompt-injection"
scope_note: "initial sweep"
agent_setting: "LLM agents with tool use and/or persistent state"
defense_approach: "semantic-isolation"
defense_type: "Semantic virtualization — isolate untrusted inputs in a virtual semantic namespace"
tags:
  - prompt-injection
  - defense
  - semantic-isolation
  - virtualization
  - architecture
categories:
  - cs.CR
---

- **One-line take:** Give untrusted data its own semantic sandbox — the model can read it but can't confuse it with instructions.
- **Defense approach:** Semantic virtualization — isolate untrusted inputs in a virtual semantic namespace
- **Pros:** Principled separation of data and instructions; works against indirect injection; no classifier needed
- **Cons:** Requires framework-level integration; may reduce model's ability to reason about untrusted content; novel, limited validation
- **Abstract-level summary:** Large Language Model (LLM) agents are increasingly used to automate complex workflows, but integrating untrusted external data with privileged execution exposes them to severe security risks, particularly direct and indirect prompt injection. Existing defenses face significant challenges in balancing security with utility, often encountering a trade-off where rigorous protection leads to over-defense, or where subtle indirect injections bypass detection. Drawing inspiration from operating system virtualization, we propose AgentVisor, a novel defense framework that enforces semantic privilege s
