---
title: "Unexpected benefits of self-modelling in neural systems"
authors:
  - Vickram Premakumar
  - Michael Vaiana
  - Florin Pop
  - Judd Rosenblatt
  - Diogo Schwerz de Lucena
  - Kirsten Ziman
  - Michael S. A. Graziano
doi: "10.1098/rsta.2024.0531"
url: "https://royalsocietypublishing.org/doi/full/10.1098/rsta.2024.0531"
published: "2026-05-14"
source: "Phil. Trans. R. Soc. A 384(2320) — theme issue 'World models in natural and artificial intelligence'"
article_type: "Research article"
read_depth: "full"
mechanism: "Adds an auxiliary task where a network predicts its own internal states ('self-modelling'); measures the effect on network complexity via weight distribution and the real log canonical threshold (RLCT). Self-modelling makes networks simpler, more regularized, more parameter-efficient."
tags:
  - self-model
  - regularization
  - singular-learning-theory
  - rlct
  - consciousness
  - graziano
categories:
  - artificial intelligence
---

- **One-line take:** Make a network predict its *own* internal states as a side task, and it restructures itself to be simpler and more predictable — self-modelling acts as self-regularization. A clean empirical result with a provocative implication for why brains (and maybe minds) model themselves. Graziano (attention-schema theory) is an author.

- **The hypothesis:** to better predict its own internal states, a network is pressured to *make those states easier to predict* — i.e. simpler, more regular, more compressible. Self-modelling isn't just introspection; it changes the system being introspected.

- **The method (why it's credible, not just a story):** across 3 architectures × 3 tasks/2 modalities (MNIST, CIFAR-10, IMDB), add a self-modelling auxiliary head and vary its training weight. Measure complexity two ways:
  1. **weight distribution** — narrower / clustered near smaller magnitudes with self-modelling (like weight-norm regularization, which aids generalization);
  2. **RLCT (real log canonical threshold)** from singular learning theory — a principled complexity measure — is *lower* with self-modelling.
  Both drop consistently → self-modelling reduces effective complexity.

- **The bigger claim (carefully hedged):** this self-regularization may explain benefits of self-models seen in ML, *and* the adaptive value of self-models in biological brains — a functional, mechanistic reason minds model themselves, independent of the consciousness debate.

- **Why it matters for us:** two angles. (1) Practical: a self-prediction auxiliary objective as a cheap regularizer. (2) Conceptual: it's the issue's "self-referential world model" exemplar — a system whose world model includes *itself*. For agents, self-modelling connecting to simplicity/predictability is suggestive for introspective agents that reason about their own state/uncertainty.

- **Abstract:** Self-models interest human-cognition and machine-learning researchers, but what benefits do they confer? When an artificial network learns to predict its internal states as an auxiliary task, it becomes simpler, more regularized and more parameter-efficient. Across architectures and three classification tasks in two modalities, adding self-modelling significantly reduced network complexity — a narrower weight distribution and a smaller RLCT — supporting the hypothesis that self-modelling has a restructuring, self-regularizing effect, which may also explain the adaptive value of self-models in brains.
