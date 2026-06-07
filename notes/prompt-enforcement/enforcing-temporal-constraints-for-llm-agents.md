---
title: "Enforcing Temporal Constraints for LLM Agents"
authors:
  - Various
arxiv_id: "2512.23738"
arxiv_url: "https://arxiv.org/abs/2512.23738"
published: "2025-12-25"
updated: "2025-12-25"
source: "arXiv"
project: "prompt-enforcement"
scope_note: "initial sweep"
agent_setting: "LLM agents in safety-critical applications with temporal ordering requirements"
mechanism: "Enforces temporal safety policies — rules about the ordering and sequencing of agent actions — through deterministic runtime checks."
tags:
  - agent-safety
  - temporal-constraints
  - runtime-enforcement
  - action-ordering
  - deterministic-enforcement
categories:
  - cs.AI
  - cs.SE
---

- **One-line take:** Agents must do A before B? Make that a deterministic constraint, not a hope.
- **How it enforces safety:** Enforces temporal safety policies — rules about the ordering and sequencing of agent actions — through deterministic runtime checks.
- **Why it matters:** Addresses a specific class of instruction violations — temporal ordering — with deterministic enforcement.
- **Caveats / limits:** Newly collected; needs deeper reading.
- **Abstract-level summary:** LLM-based agents are deployed in safety-critical applications, yet current guardrail systems fail to prevent violations of temporal safety policies, requirements that govern the ordering and sequencing of agent actions. For instance, agents may access sensitive data before authenticating users or process refunds to unauthorized payment methods, violations that require reasoning about sequences of actions rather than individual decisions.
