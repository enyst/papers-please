---
title: "Levels of analysis for large language models"
authors:
  - Alexander Ku
  - Declan Campbell
  - Xuechunzi Bai
  - Jiayi Geng
  - Ryan Liu
  - Raja Marjieh
  - R. Thomas McCoy
  - Andrew Nam
  - Ilia Sucholutsky
  - Liyi Zhang
  - Jian-Qiao Zhu
  - Thomas Griffiths
doi: "10.1098/rsta.2025.0012"
url: "https://royalsocietypublishing.org/doi/full/10.1098/rsta.2025.0012"
published: "2026-05-14"
source: "Phil. Trans. R. Soc. A 384(2320) — theme issue 'World models in natural and artificial intelligence'"
article_type: "Opinion piece"
read_depth: "full"
mechanism: "Applies David Marr's three levels of analysis (computational / algorithmic / implementation) as an organizing toolkit for understanding LLMs with cognitive-science methods."
tags:
  - interpretability
  - cognitive-science
  - marr-levels
  - llm-understanding
  - embers-of-autoregression
categories:
  - artificial intelligence
---

- **One-line take:** Treat an LLM like a mind you have to understand from the outside in — and reuse cognitive science's accumulated toolkit, organized by Marr's three levels. A clean, practical framework rather than a new result.

- **The three levels, applied to LLMs:**
  - **Computational** (what problem is it solving / what objective): the training objective *predicts behaviour*. Their headline example — **"embers of autoregression"**: because the objective is next-token prediction, LLMs show task-frequency and answer-probability sensitivities that a "reasoner" wouldn't. Also: Bayesian optimality as a benchmark, and documented violations of axiomatic systems (e.g. inconsistent preferences).
  - **Algorithmic** (what procedure/representation): borrow psychology methods — similarity judgements, parallel vs serial processing probes, association tasks that uncover hidden structure.
  - **Implementation** (the mechanism in the weights): representational analysis (probing) and causal analysis (activation patching / ablation) — i.e. mechanistic interpretability as the neuroscience of the model.

- **The useful reframing:** interpretability keeps reinventing tools psychology already built to study an opaque intelligence (the brain). Marr's levels stop people from conflating "what it does" with "how it does it" with "why (objective)" — a common category error in LLM debates.

- **Honest limit they raise (Beyond Marr's levels):** LLMs are trained, not designed, and shaped by data distribution + RLHF, so the clean computational/algorithmic split gets muddy; they flag where the analogy strains.

- **Why it matters for us:** this is the methodological companion to our interpretability notes — a scaffold for asking well-posed questions about model behaviour instead of vibes. For agent work: separating "the objective made it do this" from "it represents X" is exactly the discipline needed when debugging why an agent behaves oddly.

- **Abstract:** Modern AI systems like LLMs are increasingly powerful but hard to understand. Recognizing this as analogous to historical difficulties in understanding the human mind, the authors argue cognitive-science methods can help, and propose a framework based on Marr's levels of analysis. Revisiting established techniques relevant to each level, they aim to provide a toolkit for making sense of these new kinds of minds.
