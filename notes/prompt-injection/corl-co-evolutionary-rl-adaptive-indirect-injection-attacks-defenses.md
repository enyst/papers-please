---
title: "CoRL: Co-Evolutionary Reinforcement Learning for Adaptive Indirect Prompt-Injection Attacks and Defenses"
authors:
  - (see paper)
arxiv_id: "2609.07529"
arxiv_url: "https://arxiv.org/abs/2609.07529"
published: "2026-09"
source: "arXiv:2609.07529 [cs.CR]"
read_depth: "abstract-only"
mechanism: "Formulates adaptive indirect prompt injection as an asymmetric, partially-observable, general-sum Markov game and co-trains attacker and defender with RL (attacker SFT init → bilateral Co-PPO with role-specific rewards, verifier-grounded), producing both a hardened defender and a bank of adaptive attackers for red-teaming."
tags:
  - prompt-injection
  - indirect-prompt-injection
  - co-evolution
  - reinforcement-learning
  - red-teaming
  - defense
  - attack
categories:
  - cs.CR
---

- **One-line take:** Treats the injection arms race as a **game** and trains both sides together. Defenses trained on *fixed* attacks fail when the attacker changes strategy/site/payload; CoRL co-evolves a multi-turn attacker and a tool-using defender so the defender hardens against an adapting adversary — and you keep the evolved attackers as a red-team suite.

- **Mechanism:** adaptive IPI as an asymmetric, partially-observable, general-sum Markov game (attacker adapts payloads at reachable tool-return sites from the public trajectory; defender must block the injected objective *and* complete the user task). Three stages: Attacker SFT (init from successful trajectories) → bilateral **Co-PPO** (role-specific rewards, verifier-grounded) → repair. Balances safety vs task utility; shows transfer on external benchmarks.

- **Why it matters for us:** the training-time complement to "IPI as test-time search" (2609.04495) — both say static defenses are a mirage against adaptive attackers. The keep-the-attackers-for-red-teaming idea is directly reusable: an evolving adversary bank to test SmolPaws' resistance rather than a fixed attack list.

- **Source:** abstract via arXiv:2609.07529 (Chrome). Not yet full-read.
