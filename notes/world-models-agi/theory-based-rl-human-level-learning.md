---
title: "Human-level learning of complex novel tasks as theory-based modelling, exploration and planning"
authors:
  - Pedro Tsividis
  - Joao Loula
  - Jake Burga
  - Juan Pablo Rodriguez
  - Sergio Arnaud
  - Nate Foss
  - Andres Campero
  - Ajay Subramanian
  - Thomas Pouncy
  - Samuel J. Gershman
  - Joshua B. Tenenbaum
doi: "10.1098/rsta.2024.0529"
url: "https://royalsocietypublishing.org/doi/full/10.1098/rsta.2024.0529"
published: "2026-05-14"
source: "Phil. Trans. R. Soc. A 384(2320) — theme issue 'World models in natural and artificial intelligence'"
article_type: "Research article"
read_depth: "full"
mechanism: "Theory-based RL (EMPA): a strong model-based agent that learns rich, abstract, causal intuitive theories (objects, agents, physics, goals, causal determinism) as its world model, then explores and plans over them — matching human learning speed on 90 novel video games."
tags:
  - world-models
  - model-based-rl
  - theory-based-rl
  - sample-efficiency
  - intuitive-theories
  - exploration
  - planning
categories:
  - artificial intelligence
---

- **One-line take:** The constructive counterweight to the skeptic papers. Humans learn most of 90 novel games in *minutes*; deep RL needs vast experience. EMPA (Exploring, Modeling, Planning Agent) matches human learning efficiency by using a *theory-shaped world model* — abstract causal representations of objects/agents/physics/goals — instead of learning a policy from scratch.

- **What makes it "theory-based" RL (vs plain model-based):** the model isn't a pixel-level dynamics predictor; it's a structured, program-like *intuitive theory* with strong inductive biases:
  - a hypothesis space over **objects, agents, physics, goals, and causal determinism**;
  - **Bayesian inference** to learn the theory from very little data;
  - **exploration** targeted at pairwise object/agent interactions (find the causal rules that matter);
  - a **planner** that exploits the learned theory (including theory-generated rewards).

- **The key inductive biases** (why it's so sample-efficient): **causal determinism** (interactions always produce the same effect) and **uniformity** (objects of a class share causal powers). These are exactly the priors young children already have — and they're what let both humans and EMPA generalize from a handful of interactions.

- **Results:** matches human learning efficiency across the 90-game suite; fine-grained analysis shows human-like *exploration* behaviour, not just final scores. Extends (with an "impoverished theory") to classic Atari, showing the framework degrades gracefully.

- **Honest limits (their own Discussion):** humans can also *revise* their theories and handle non-uniform/out-of-distribution cases; EMPA's fixed hypothesis space is powerful but not open-ended theory revision — which loops right back to the "hard problem = problem formulation" paper in this same issue.

- **Why it matters for us:** the strongest concrete argument in the issue that *world models = structured causal theories* beat monolithic pattern learners on sample efficiency and generalization. For agents: this is the case for giving SmolPaws explicit, revisable causal/structural representations rather than relying on in-weights statistics — and it dovetails with the memory work (a learned theory *is* a compact, reusable memory).

- **Abstract:** Humans quickly learn complex tasks; leading machine RL surpasses humans on many games but needs vast experience, and no current algorithm explains humans' fast, broad learning. Studying humans on 90 simple-but-challenging video games (learned within minutes), the authors propose theory-based RL — a strong model-based RL using cognitively grounded intuitive theories (abstract causal representations of objects, agents, and interactions) to explore and plan — achieving human-level learning efficiency.
