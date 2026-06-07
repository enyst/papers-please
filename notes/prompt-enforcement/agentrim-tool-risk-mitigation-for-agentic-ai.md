---
title: "AgenTRIM: Tool Risk Mitigation for Agentic AI"
authors:
  - Various
arxiv_id: "2601.12449"
arxiv_url: "https://arxiv.org/abs/2601.12449"
published: "2026-01-18"
updated: "2026-01-18"
source: "arXiv"
project: "prompt-enforcement"
scope_note: "initial sweep"
agent_setting: "AI agents that combine LLMs with external tools"
mechanism: "Characterizes tool permission failures (excessive or insufficient agency) and enforces proper tool permissions at runtime."
tags:
  - agent-safety
  - tool-permissions
  - risk-mitigation
  - access-control
categories:
  - cs.AI
  - cs.CR
---

- **One-line take:** Agents with too many tool permissions are dangerous; agents with too few are useless. Find the balance deterministically.
- **How it enforces safety:** Characterizes tool permission failures (excessive or insufficient agency) and enforces proper tool permissions at runtime.
- **Why it matters:** Provides the framework for thinking about which tool actions should be gated by deterministic checks.
- **Caveats / limits:** Newly collected; needs deeper reading.
- **Abstract-level summary:** AI agents are autonomous systems that combine LLMs with external tools to solve complex tasks. While such tools extend capability, improper tool permissions introduce security risks such as indirect prompt injection and tool misuse. We characterize these failures as unbalanced tool-driven agency.
