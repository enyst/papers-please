---
title: "Artificial intelligence for science: the easy and hard problems"
authors:
  - (see paper)
doi: "10.1098/rsta.2024.0530"
url: "https://royalsocietypublishing.org/doi/full/10.1098/rsta.2024.0530"
published: "2026-05-14"
source: "Phil. Trans. R. Soc. A 384(2320) — theme issue 'World models in natural and artificial intelligence'"
article_type: "Opinion / perspective"
read_depth: "full"
mechanism: "Separates AI-for-science into the 'easy problem' (optimize a pre-specified objective on a dataset) and the 'hard problem' (invent/refine the problem itself — conceptual revision), and argues the hard problem is out of reach for current algorithms."
tags:
  - concept-formation
  - scientific-discovery
  - paradigm-revision
  - world-models
  - cognitive-science-of-scientists
categories:
  - artificial intelligence
---

- **One-line take:** The most Engel-relevant paper in the issue. AI has crushed the "easy problem" of science (optimize a well-posed objective — AlphaFold, antibiotics, fusion designs), but the "hard problem" is *formulating the problem* — "the problem problem" — and that needs continual conceptual revision under poorly-defined constraints, which no current system does.

- **The core distinction:**
  - **Easy problem** = the *form of the problem is given*: inputs, outputs, and a loss to compare against ground truth are specified up front. Hard in engineering effort, easy in *kind*. This is where all the flashy AI-for-science wins live.
  - **Hard problem** = coming up with the problem. "Great scientists are not extraordinary optimizers of ordinary problems; they are ordinary optimizers of extraordinary problems." Einstein didn't have a better function approximator — he reformulated what the question was.

- **Sharp move — the hard problem isn't just "revolutionary science":** they argue even *normal* science (a grad student deciding what's worth working on: which pathway is functionally important, can be isolated, admits a formalism) is problem-*formulation*, not optimization. So the barrier isn't rare — it's everywhere, and it's the same barrier for AI scientists and humans. Grounds it in Popper & Laudan on the primacy of problem proposal/refinement.

- **The prescription:** study the *cognitive science of scientists* — how humans actually infer and revise paradigms — then build computational agents that automatically infer and update their scientific paradigms (not just solve within a fixed one).

- **Why it matters for us:** this is the crisp articulation of the concept-formation gap. For an agent (SmolPaws) the analogue is: current agents execute well-specified tasks (easy) but don't reframe the task, notice the wrong frame, or invent the right abstraction (hard). Directly connects to Engel's "concept formation" interest and to the memory question — paradigm revision is a *memory-and-representation-restructuring* problem.

- **Abstract:** Recent AI-driven scientific discoveries almost all result from training flexible algorithms to solve difficult optimization problems specified in advance by domain scientists with large datasets. Useful, but only one part of science — the 'easy problem'. The other part is coming up with the problem itself — the 'hard problem' — which is beyond current discovery algorithms because it requires continual conceptual revision based on poorly defined constraints. Progress can come from studying the cognitive science of scientists and using the results to design agents that automatically infer and update their scientific paradigms.
