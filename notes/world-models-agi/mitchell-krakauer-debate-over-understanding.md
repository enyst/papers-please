---
title: "The Debate Over Understanding in AI's Large Language Models"
authors:
  - Melanie Mitchell
  - David C. Krakauer
doi: "10.1073/pnas.2215907120"
arxiv_id: "2210.13966"
url: "https://arxiv.org/abs/2210.13966"
source_pdf: "https://arxiv.org/pdf/2210.13966"
published: "2023-02 (PNAS 120(13); arXiv Oct 2022)"
source: "PNAS, Vol. 120, No. 13 (2023), e2215907120"
article_type: "Survey / perspective"
read_depth: "full (pulled full text)"
mechanism: "Surveys the for/against arguments on whether LLMs 'understand', diagnoses the split as statistical-correlation models of cognition vs causal-mechanism models, and argues for an extended science of intelligence that recognizes distinct, possibly non-human modes of understanding."
tags:
  - understanding
  - llm
  - debate
  - statistics-vs-causal
  - science-of-intelligence
  - grounding
categories:
  - artificial intelligence
---

- **One-line take:** The best single map of the exact fault line the RSTA issue runs on — written by two of that issue's own editors. It lays out both camps fairly and reframes the disagreement as a deeper split: **understanding-as-statistical-correlation** vs **understanding-as-causal-mechanism**. Its constructive proposal: stop asking the yes/no question and build a *science of intelligence* that admits multiple, possibly alien, modes of understanding.

- **The two camps, steelmanned:**
  - **"They don't understand"** — LLMs learn correlations among tokens; humans use *compressed concepts grounded in real-world experience*. Brittleness, unpredictable errors, and weak robust generalization are the tells (they cite the grounding/embodiment tradition — Harnad, Bender & Koller are in this lineage).
  - **"They understand (or something like it)"** — competence at scale on open-ended language/reasoning tasks is not nothing; maybe there's a new, non-human kind of understanding emerging.
  - Both sides have strong intuitions; the authors' point is that **our current tests can't adjudicate**.

- **The methodological warning (the sharp bit):** researchers apply psychological tests (theory-of-mind, reasoning) built for humans to LLMs and read human-like scores as human-like understanding. But those tests are only valid *proxies under assumptions about human cognition that may be false for LLMs* — a model with an "unimaginable capacity to learn correlations" can pass a human proxy without the underlying competence. So benchmark passes are weak evidence; we need probes designed for "exotic, mind-like entities."

- **The reframe:** LLMs may be a genuinely new "species" in a larger zoo of intelligences — like AlphaZero/AlphaFold bringing an "alien intuition" to chess/protein-folding. The future work is a science that reveals the *mechanisms* of understanding across distinct intelligences, maps their strengths/limits, and learns to integrate statistical and causal modes.

- **Why it's foundational to this issue:** this is the direct precursor and companion to RSTA 384(2320) — the intro paper's "statistical surface regularities vs grounded understanding" spine is this paper's thesis, and the **l33t-task**, **emergence**, and **theory-based RL** papers are all attempts at the sharper probes it calls for. Read it right after the issue intro.

- **Why it matters for us:** it's the honest posture for anyone building agents — don't declare "the model understands" from fluent output (Turing's standard failing at scale), and don't declare "just statistics" either; instead design *discriminating probes* and expect non-human modes. It also gives the "statistical vs causal" axis that connects straight to the empowerment / theory-based-RL / causal-world-model thread we care about.

- **Source:** full text pulled via jina from arXiv:2210.13966 (PNAS 2023); linked above.
