---
title: "Agent libOS: A Library-OS-Inspired Runtime for Long-Running, Capability-Controlled LLM Agents"
authors:
  - Various
arxiv_id: "2606.03895"
arxiv_url: "https://arxiv.org/abs/2606.03895"
published: "2026-06-02"
updated: "2026-06-02"
source: "arXiv"
project: "prompt-enforcement"
scope_note: "initial sweep"
agent_setting: "long-running LLM agents that maintain state, fork subtasks, and perform side effects"
mechanism: "Provides OS-level capability isolation — agents run within a runtime that controls what resources and actions are permitted, like a library OS."
tags:
  - agent-safety
  - capability-control
  - runtime
  - os-inspired
  - isolation
categories:
  - cs.AI
  - cs.OS
---

- **One-line take:** Give the agent an OS with capability controls instead of trusting it to police itself.
- **How it enforces safety:** Provides OS-level capability isolation — agents run within a runtime that controls what resources and actions are permitted, like a library OS.
- **Why it matters:** The systems-level complement to instruction enforcement — control the execution environment itself.
- **Caveats / limits:** Newly collected; needs deeper reading.
- **Abstract-level summary:** Large language model (LLM) agents are evolving from request-response assistants into long-running software actors: they maintain state across model calls, fork subtasks, wait for external events, request human authority, generate tools, and perform side effects that must be resumed and audited. This paper presents Agent libOS, a library-OS-inspired runtime substrate for LLM agents.
