---
title: "Position: AI Safety Requires Effective Controllability"
authors:
  - Various
arxiv_id: "2605.27117"
arxiv_url: "https://arxiv.org/abs/2605.27117"
published: "2026-05-26"
updated: "2026-05-26"
source: "arXiv"
project: "prompt-enforcement"
scope_note: "initial sweep"
agent_setting: "position paper on AI safety in open-ended, interactive, tool-using environments"
mechanism: "Argues that alignment (training models to follow preferences) is insufficient — deployed agents need effective controllability: the ability to be stopped, overridden, or constrained deterministically."
tags:
  - agent-safety
  - controllability
  - position-paper
  - alignment-limits
categories:
  - cs.AI
---

- **One-line take:** Aligned behavior is not controllable behavior. You need deterministic overrides, not just good training.
- **How it enforces safety:** Argues that alignment (training models to follow preferences) is insufficient — deployed agents need effective controllability: the ability to be stopped, overridden, or constrained deterministically.
- **Why it matters:** Theoretical foundation for the entire prompt-shield idea: alignment is probabilistic, controllability must be deterministic.
- **Caveats / limits:** Newly collected; needs deeper reading.
- **Abstract-level summary:** AI safety is still largely framed as alignment: training models to follow human preferences, safety policies, and normative constraints. That framing has improved the behavior of modern language models, but aligned behavior does not by itself guarantee that a deployed agent can be stopped, overridden, or constrained once it operates in open-ended, interactive, and tool-using environments.
