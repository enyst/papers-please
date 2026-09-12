---
title: "On the representation complexity of model-based and model-free reinforcement learning"
authors:
  - (see paper)
doi: "10.1098/rsta.2024.0532"
url: "https://royalsocietypublishing.org/doi/full/10.1098/rsta.2024.0532"
published: "2026-05-14"
source: "Phil. Trans. R. Soc. A 384(2320) — theme issue 'World models in natural and artificial intelligence'"
article_type: "Research article (theory)"
read_depth: "abstract-only"
mechanism: "Circuit-complexity analysis: a broad class of MDPs has transition+reward representable by polynomial-size constant-depth circuits, while the optimal Q-function needs exponential-size constant-depth circuits — a representation-complexity reason model-based RL is more sample-efficient than model-free."
tags:
  - model-based-rl
  - world-models
  - circuit-complexity
  - sample-efficiency
  - theory
categories:
  - artificial intelligence
---

- **One-line take:** A rigorous why-world-models-help result: for a broad MDP class, the *model* (transition + reward) is cheap to represent (poly-size, constant-depth circuits) while the *optimal Q-function* is exponentially expensive at constant depth. So model-based RL's sample-efficiency edge has a representation-complexity explanation — sometimes the rule of the world is simple even when the value function is not.

- **Why it's worth logging:** it's the formal/complexity-theory counterpart to the issue's empirical "world models beat model-free" story (theory-based RL paper). Corroborated empirically in MuJoCo: approximation errors of transition kernel and reward are consistently lower than for the optimal Q-function. Claims to be the first circuit-complexity study of RL.

- **Status:** abstract-only — it's a solid, narrow theory result; I logged it at abstract depth because the takeaway ("model simple, value complex → prefer model-based") is fully carried by the abstract + the theory-based-RL note. **Flag:** full read if we want the proof structure.

- **Abstract:** The authors study representation complexity of model-based vs model-free RL via circuit complexity, proving a broad class of MDPs whose transition and reward functions are representable by polynomial-size constant-depth circuits, whereas the optimal Q-function has exponential complexity at constant depth. This gives a novel representation-complexity reason model-based algorithms enjoy better sample complexity: the ground-truth model can be simple while quantities like the Q-function are complex. Empirically corroborated across MuJoCo environments (transition/reward approximation errors consistently below the optimal Q-function's).
