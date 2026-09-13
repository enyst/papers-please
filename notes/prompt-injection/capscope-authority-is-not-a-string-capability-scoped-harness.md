---
title: "Authority Is Not a String: A Capability-Scoped Harness for Prompt-Injection-Resistant Coding Agents (CapScope)"
authors:
  - (see paper)
arxiv_id: "2609.08371"
arxiv_url: "https://arxiv.org/abs/2609.08371"
published: "2026-09"
source: "arXiv:2609.08371 [cs.CR]"
read_depth: "abstract-only"
mechanism: "CapScope: a harness-level authorization layer. It derives a task-wide 'authority ceiling' from trusted input, gives each (sub-)agent typed capabilities stored OUTSIDE the model context, and checks every tool call against the issuing agent's capabilities — so an injection can request an action but can't get authority it wasn't granted."
tags:
  - prompt-injection
  - indirect-prompt-injection
  - capability-security
  - coding-agents
  - harness
  - defense
  - ambient-authority
categories:
  - cs.CR
---

- **One-line take:** The best-aligned new defense for us — kill prompt injection at the **authorization** layer, not the detection layer. Coding-agent tools carry *ambient authority* (naming a resource is enough to act on it); CapScope replaces that with **typed capabilities held outside the model's context**, checked per tool call. An injected instruction can *ask*, but the request is blocked unless that agent already holds the capability. No need to detect malicious text at all.

- **Mechanism:** before any repo content / tool output is read, derive a task-wide **authority ceiling** from trusted input; assign each agent a separate capability set (kept out of context so injection can't grant itself more); check every call. Sub-agent permissions don't leak to peers.

- **Result:** on the Pi coding agent, orchestrator→sub-agent repair workflow, 300 runs (5 tasks × 5 injection surfaces × 4 auth conditions × 3 trials): injected effect fired **33–47/75** under ambient-authority / global-policy baselines vs **3/75** under CapScope, while still completing 68/75 repairs (baselines 68–72/75). Big security win, negligible utility cost.

- **Why it matters for us:** directly actionable for SmolPaws' own multi-agent/automation setup — capability-scoping per sub-agent is a design pattern, not a model tweak, and it's the "hard boundary, not soft guardrail" approach (cf. `agentic-engineering/fences-not-sandboxes`). Ties the prompt-injection and harness atlases together. Strong candidate for a **full read**.

- **Source:** abstract via arXiv:2609.08371 (Chrome). Not yet full-read.
