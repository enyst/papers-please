---
title: "Empowerment gain and causal model construction: children and adults are sensitive to controllability and variability in their causal interventions"
authors:
  - Eunice Yiu
  - Kelsey Allen
  - Shiry Ginosar
  - Alison Gopnik
doi: "10.1098/rsta.2025.0003"
url: "https://royalsocietypublishing.org/doi/full/10.1098/rsta.2025.0003"
published: "2026-05-14"
source: "Phil. Trans. R. Soc. A 384(2320) — theme issue 'World models in natural and artificial intelligence'"
article_type: "Research article"
read_depth: "full"
mechanism: "Proposes 'empowerment' (an intrinsic RL reward = mutual information between actions and outcomes) as the bridge between Bayesian causal-model learning and RL: accurate causal world models raise empowerment, and seeking empowerment builds better causal models. Tested empirically in children and adults."
tags:
  - causal-learning
  - empowerment
  - intrinsic-motivation
  - world-models
  - developmental
  - active-learning
categories:
  - artificial intelligence
---

- **One-line take:** Gopnik's group argues **empowerment** — an intrinsic reward maximizing mutual information between your actions and their outcomes — is the missing bridge between two traditions: Bayesian causal-Bayes-net learning and reinforcement learning. Their claimed equivalence: an accurate causal world model *necessarily* raises empowerment, and *seeking* empowerment drives you to a more accurate causal model.

- **Why the bridge is interesting:** causal learning has been hard for large pretrained models with standard deep learning; cognitive scientists model it well with causal Bayes nets but that's not obviously trainable at scale. Empowerment is a *single scalar intrinsic signal* an RL agent can optimize — so it's a computationally tractable route to the causal-model-building that deep learning lacks. It reframes "learn causal structure" as "maximize controllable influence over outcomes."

- **The developmental angle:** empowerment-seeking may explain distinctive features of children's causal learning — their drive to *control* things is not noise, it's the objective that builds the world model. Children as empowerment maximizers.

- **The experiments (star machines):** systematically test whether children and adults use cues to **empowerment** — controllability and variability of outcomes — to (a) infer causal relations and (b) design effective interventions. Both groups are sensitive to controllability/variability, consistent with empowerment guiding causal exploration.

- **Why it matters for us:** a concrete, optimizable objective for an agent that *wants to understand* rather than just predict — directly relevant to concept formation and to exploration policy in agents. "Prefer actions whose outcomes you can reliably control/predict" is a memorable design heuristic for autonomous agents, and it ties to the theory-based-RL paper's exploration story (both target the causal structure that matters).

- **Abstract:** Causal learning is fundamental to cognition and hard for large pretrained models. Cognitive scientists use the causal Bayes net formalism to model human causal learning; RL describes an intrinsic reward, 'empowerment', maximizing mutual information between actions and outcomes. Empowerment may bridge Bayesian causal learning and RL: an accurate causal world model necessarily increases empowerment, and increasing empowerment yields a more accurate causal model. It may also explain features of children's causal learning and provide a tractable computational account. An empirical study tests how children and adults use cues to empowerment to infer causal relations and design interventions.
