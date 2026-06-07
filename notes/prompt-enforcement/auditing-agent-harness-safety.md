---
title: "Auditing Agent Harness Safety"
authors:
  - Various
arxiv_id: "2605.14271"
arxiv_url: "https://arxiv.org/abs/2605.14271"
published: "2026-05-14"
updated: "2026-05-14"
source: "arXiv"
project: "prompt-enforcement"
scope_note: "initial sweep"
agent_setting: "LLM agents running inside execution harnesses that dispatch tools and route messages"
mechanism: "Evaluates safety of the execution harness itself — not just the model output but the trajectory of tool calls and resource access."
tags:
  - agent-safety
  - harness-auditing
  - trajectory-safety
  - tool-dispatch
categories:
  - cs.CR
  - cs.AI
---

- **One-line take:** A correct answer from an unsafe trajectory is still a security failure.
- **How it enforces safety:** Evaluates safety of the execution harness itself — not just the model output but the trajectory of tool calls and resource access.
- **Why it matters:** Motivates why hooks and enforcement must be at the harness level, not just the output level.
- **Caveats / limits:** Newly collected; needs deeper reading.
- **Abstract-level summary:** LLM agents increasingly run inside execution harnesses that dispatch tools, allocate resources, and route messages between specialized components. However, a harness can return a correct, benign answer over a trajectory that accesses unauthorized resources or leaks context to the wrong agent.
