# Continual Harness: Online Adaptation for Self-Improving Foundation Agents

**Paper:** [arXiv:2605.09998](https://arxiv.org/abs/2605.09998)
**Authors:** Seth Karten, Joel Zhang, Tersoo Upaa Jr, Ruirong Feng, Wenzhe Li, Chengshuai Shi, Chi Jin, Kiran Vodrahalli
**Date:** 2026-05-11
**Subjects:** cs.LG; cs.AI
**Type:** Self-improving harness for embodied agents + online co-learning loop

## One-Line Summary

A **reset-free** self-improving harness for long-horizon, partially-observable (embodied) agents: while it runs — no episode resets — the agent alternates between **acting** and **refining its own prompt, sub-agents, skills, and memory** from any past trajectory. Then it closes the loop back onto the weights with an online process-reward co-learning step.

## The Story (why it exists)

Coding harnesses (Claude Code, OpenHands) wrap a model with tools/memory/planning, but there was **no equivalent for embodied, long-horizon, partial-observability decision-making**. The authors first ran **Gemini Plays Pokémon (GPP)** with iterative human-in-the-loop harness refinement — the first AI to finish Pokémon Blue, Yellow Legacy (hard mode), and Crystal without a lost battle. In the hardest stages the agent started **iterating on its own strategy** via long-context memory — emergent self-improvement. Continual Harness formalizes and automates exactly that, removing the human from the loop.

## The Method

Two nested loops:
1. **Online harness refinement (reset-free).** From only a **minimal environment interface** — no curated knowledge, no hand-crafted tools, no domain scaffolding — the agent alternates act ↔ refine, mutating prompt / sub-agents / skills / memory using any past trajectory data. The key distinction from prompt-optimization methods (DSPy, GEPA, Reflexion-style): those **require episode resets**; Continual Harness adapts **online within a single run**.
2. **Process-reward co-learning (closing onto the model).** An open-source agent's rollouts through the refining harness are **relabeled by a frontier teacher** and used to **update the model** — driving sustained in-game milestone progress on Pokémon Red **without resetting the environment** between training iterations. This is the "test-time training" step the authors call the direction that matters most.

## Key Results

- Pokémon Red & Emerald, across frontier models: starting **from scratch** (raw interface), Continual Harness substantially cuts button-press cost vs. the minimalist baseline and **recovers a majority of the gap** to a hand-engineered expert harness — gains scale with model capability.
- The co-learning loop yields **sustained milestone progress on Pokémon Red** with no environment resets between training iterations.
- GPP milestone: first system to complete Blue / Yellow Legacy hard mode / Crystal without a lost battle (human-in-the-loop precursor).

## Why It Matters (for us)

The far end of the DAIR.AI [Harness Engineering](../../blogs/interesting-posts.md) genealogy — "the last step before online learning." Where Meta-Harness (`meta-harness-end-to-end-optimization-of-model-harnesses.md`) and Darwin Gödel Machine (`darwin-godel-machine-open-ended-evolution-self-improving-agents.md`) optimize a harness **between** runs, Continual Harness mutates it **during** the run and then feeds experience back into the weights. Two takeaways for OpenHands:
- **Reset-free online adaptation** is a different regime from our current condense/summarize loop — it argues for treating the harness (skills, sub-agent specs, memory) as live, mutable state during a single long task, not just across tasks. Rhymes with SKILL.state (`skill-state-scalable-long-horizon-agent-skills.md`) and our notes+retrieval condensation idea.
- **Teacher-relabeled rollouts → weight update** is the bridge from harness engineering to actual training; relevant to the Liberty-Labs open-weight thesis (close the gap on an open model using a frontier teacher + a good harness, cf. OpenJarvis' ~800× cost argument).
- Same lead author (Seth Karten) as **Prime Agent** (pointered in `skill-state-...md`); Continual Harness is the embodied/online sibling of that coding-harness work.

## Caveats / Limits

- Evaluated in **game** environments (Pokémon) — external validity to software/agentic-coding tasks is unestablished.
- The co-learning loop needs a **frontier teacher** to relabel rollouts, so "self-improving" still leans on a stronger external model.
- Reset-free online mutation of prompts/skills/sub-agents raises stability/safety questions the paper only begins to address.
