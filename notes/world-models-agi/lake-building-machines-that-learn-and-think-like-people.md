---
title: "Building Machines That Learn and Think Like People"
authors:
  - Brenden M. Lake
  - Tomer D. Ullman
  - Joshua B. Tenenbaum
  - Samuel J. Gershman
doi: "10.1017/S0140525X16001837"
arxiv_id: "1604.00289"
url: "https://arxiv.org/abs/1604.00289"
source_pdf: "https://arxiv.org/pdf/1604.00289"
published: "2017 (BBS 40; arXiv Apr 2016)"
source: "Behavioral and Brain Sciences, Vol. 40 (2017), e253 (with open peer commentary)"
article_type: "Target article / manifesto"
read_depth: "full (pulled full text)"
mechanism: "Argues human-like intelligence rests on (1) 'developmental start-up software' — intuitive physics and intuitive psychology as core domains — and (2) learning as rapid model-building via compositional, causal program induction with learning-to-learn, not pattern recognition from massive data."
tags:
  - concept-formation
  - intuitive-physics
  - intuitive-psychology
  - program-induction
  - compositionality
  - causality
  - learning-to-learn
  - model-building
categories:
  - artificial intelligence
---

- **One-line take:** The manifesto for the whole "world model = structured causal theory" program — and the paper directly behind the RSTA **theory-based RL** note. Its thesis: humans don't learn by pattern-matching over huge data; we **build causal, compositional models** fast, bootstrapped by innate "start-up software" (intuitive physics + psychology). If you want machines that learn and think like people, engineer *those* ingredients, don't just scale.

- **The two "developmental start-up software" domains** (the innate priors that make fast learning possible):
  - **Intuitive physics** — infants track objects, expect solidity/persistence/continuity, discount impossible trajectories. A rough physics engine in the head.
  - **Intuitive psychology** — infants read agents as having goals and beliefs, acting efficiently toward goals.
  - These priors are why a human can learn a new video game in minutes (cf. theory-based RL): you don't start from pixels, you start from objects-with-causal-powers and goal-directed agents.

- **The three learning ingredients they argue AI needs:**
  1. **Compositionality** — build rich representations by combining reusable parts (concepts as programs assembled from primitives).
  2. **Causality** — represent the *generative process* that produces observations, not just correlations (a concept is a causal model of how examples are made).
  3. **Learning-to-learn** — prior learning reconfigures the hypothesis space so new concepts need very little data. Transfer as a first-class mechanism.
  - Learning = **rapid model-building**, not incremental function approximation.

- **The framing contrast (still the live debate):** "pattern recognition vs model building." Deep nets (then and now) excel at the former; humans do the latter, which is why humans generalize from one or a few examples and machines need thousands. They're careful to say neural nets are useful *components*, not the whole story — the ingredients can be hybridized with deep learning (as later neurosymbolic work does).

- **Why it's foundational to this issue:** it's the intellectual parent of RSTA's **theory-based RL** (EMPA), **empowerment/causal-model** (Gopnik), and **representation-complexity** papers — all instances of "structured causal world models beat monolithic statistics on sample efficiency and generalization." Read this as the *why*, and theory-based RL as the *demonstration*. It's also the constructive counter-program to Bender/Harnad skepticism: not "text can't mean," but "here's the machinery meaning-capable learning would need."

- **Why it matters for us (Engel's concept-formation interest):** this is arguably the most on-target paper in the whole set for "how do concepts form." It gives concrete design targets for an agent that *forms concepts* rather than retrieves them: compositional + causal + learning-to-learn, seeded by strong priors. It reframes memory too — a good memory isn't stored episodes but *learned causal models* that compress and transfer (dovetails with `notes/memory/`).

- **Source:** full text pulled via jina from arXiv:1604.00289 (BBS 2017); linked above.
