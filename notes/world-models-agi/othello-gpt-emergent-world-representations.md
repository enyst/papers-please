---
title: "Emergent World Representations: Exploring a Sequence Model Trained on a Synthetic Task (Othello-GPT)"
authors:
  - Kenneth Li
  - Aspen K. Hopkins
  - David Bau
  - Fernanda Viégas
  - Hanspeter Pfister
  - Martin Wattenberg
arxiv_id: "2210.13382"
url: "https://arxiv.org/abs/2210.13382"
source_pdf: "https://arxiv.org/pdf/2210.13382"
published: "2023 (ICLR 2023 notable-top-5%; arXiv Oct 2022)"
source: "ICLR 2023"
article_type: "Research article (empirical)"
read_depth: "full (pulled full text)"
mechanism: "Trains a GPT only on legal Othello move sequences (no board, no rules given), then uses probes + causal interventions to show the network builds an internal representation of board state that causally drives its predictions — an emergent world model from next-token training."
tags:
  - world-models
  - emergent-representations
  - probing
  - causal-intervention
  - interpretability
  - othello-gpt
  - understanding
categories:
  - artificial intelligence
---

- **One-line take:** The strongest empirical challenge to "it's just surface statistics." Train a GPT purely to predict the next *move token* in Othello games — never showing it a board or the rules — and it turns out to have built an internal model of the **board state** that you can (a) read out with a probe and, crucially, (b) *edit* to causally change its predictions. Next-token training can induce a genuine, manipulable **world model**.

- **The setup (why it's clean):** a synthetic, fully-known world (Othello) removes confounds — there's an objective ground-truth board state to probe against, and the model only ever sees move sequences. So any board representation is *emergent*, not memorized from board diagrams.

- **The two-step evidence (this is what makes it convincing, not just suggestive):**
  1. **Probing** — a **non-linear** probe predicts the current board state from internal activations with high accuracy (linear probes do *poorly* — a detail that matters: the world model is there but non-linearly encoded). Correlation alone, so far.
  2. **Causal intervention** — they *edit the activations* to represent a different board state, and the model's move predictions change accordingly. That upgrades the probe from "correlated readout" to "the representation is actually being *used*." They also build "latent saliency maps" to explain predictions.

- **The careful reading (the honest caveats):** Othello is tiny, deterministic, fully observable, and synthetic — a long way from natural language and the messy real world. "Emergent world representation of a board" is not "grounded understanding of meaning." And later work (Nanda et al.) refined the finding: the representation is better described as *"my pieces vs opponent's pieces"* than absolute board colour — the world model is real but not exactly the human ontology. So: strong existence proof, modest scope.

- **Why it's foundational to this issue:** it's the empirical counterweight the skeptic classics (Searle, Harnad, Bender & Koller) have to reckon with, and the concrete instance of what the RSTA **intro** and **levels-of-analysis** papers mean by looking *inside* for world models. Where the l33t-task paper is evidence *against* grounded understanding, Othello-GPT is evidence *for* emergent internal models — hold them together, don't pick one.

- **Why it matters for us:** it reframes "does the agent model the world?" as an **empirical, probe-and-intervene** question rather than a philosophical one — the same discipline as the interpretability notes (`notes/interpretability/`) and the Marr "implementation level." For agents: internal task/world state may already exist in-weights; the leverage is learning to read and *steer* it, not assuming it's absent because training was "just prediction."

- **Source:** full text pulled via jina from arXiv:2210.13382 (ICLR 2023); linked above.
