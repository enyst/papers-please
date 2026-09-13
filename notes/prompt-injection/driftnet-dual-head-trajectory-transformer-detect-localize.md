---
title: "DriftNet: A Dual-Head Trajectory Transformer for Detecting and Localizing Prompt Injection in LLM Agents"
authors:
  - (see paper)
arxiv_id: "2609.10892"
arxiv_url: "https://arxiv.org/abs/2609.10892"
published: "2026-09"
source: "arXiv:2609.10892 [cs.CR]"
read_depth: "abstract-only"
mechanism: "A <2M-param dual-head Transformer over logged tool-call trajectories: head 1 classifies the trajectory as compromised or not; head 2 labels every step (benign / injection point / hijacked / failed injection). Model-agnostic (frozen sentence encoder + identity-free per-step features); no access to the agent's model needed."
tags:
  - prompt-injection
  - indirect-prompt-injection
  - detection
  - localization
  - agent-trajectories
  - defense
categories:
  - cs.CR
---

- **One-line take:** The detector for the AgentDrift benchmark — and it answers the three questions an operator actually has in **one forward pass**: is this trace compromised, *where* did the attack enter, and *which* steps did it corrupt (incl. distinguishing resisted attacks). First supervised detector to produce this joint trace-verdict + per-step labeling.

- **Design:** tiny (<2M params) dual-head trajectory Transformer; frozen sentence encoder + four identity-free "world features" per step; class-weighted joint objective. **Model-agnostic** — reads logged tool-call trajectories, needs no access to the agent's weights. Cheap to run alongside any agent.

- **Results (AgentDrift task-disjoint split):** trajectory F1 **0.983**; exact injection-point recovery on **98.7%** of attacked traces; hijacked-span IoU 0.979; **zero** false flags on 218 resisted attacks; 2.9% on hard negatives. Big margins over a surface baseline (partial-hijack recovery 98.6% vs 11.1%). Honest caveat in their error analysis: most residual misses are traces whose labeled injection observation carries *no legible instruction*, and results ride on the benchmark's "world-identity regularity" (synthetic).

- **Why it matters for us:** a practical, model-agnostic monitor that could read SmolPaws' own tool-call logs to flag/localize a hijack — post-hoc defense complementing CapScope's preventive one. Note the synthetic-benchmark caveat before trusting the 0.98s on real traffic.

- **Source:** abstract via arXiv:2609.10892 (Chrome). Not yet full-read.
