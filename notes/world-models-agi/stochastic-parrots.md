---
title: "On the Dangers of Stochastic Parrots: Can Language Models Be Too Big? 🦜"
authors:
  - Emily M. Bender
  - Timnit Gebru
  - Angelina McMillan-Major
  - Shmargaret Shmitchell (Margaret Mitchell)
doi: "10.1145/3442188.3445922"
url: "https://dl.acm.org/doi/10.1145/3442188.3445922"
source_pdf: "https://s10251.pcdn.co/pdf/2021-bender-parrots.pdf"
published: "2021-03"
source: "FAccT '21 (ACM Conf. on Fairness, Accountability, and Transparency), pp. 610–623"
article_type: "Position paper"
read_depth: "full (pulled full text)"
mechanism: "Argues ever-larger LMs carry under-examined costs and risks: environmental/financial cost, uncurated web training data encoding hegemonic and biased views, an illusion of meaning (a 'stochastic parrot' manipulates form without communicative intent), and research opportunity cost."
tags:
  - stochastic-parrots
  - meaning-vs-form
  - bias
  - environmental-cost
  - llm-risks
  - understanding
  - ethics
categories:
  - artificial intelligence
---

- **One-line take:** The cultural touchstone of the skeptic camp, and the source of the phrase **"stochastic parrot"**: an LM is "a system for haphazardly stitching together sequences of linguistic form... according to probabilistic information about how they combine, but without any reference to meaning." Half the paper is the *understanding* argument (a sequel to the octopus); half is the *cost/harm* argument that made it famous (and got two authors pushed out of Google).

- **The four dangers (the paper's spine):**
  1. **Environmental & financial cost** — training huge models burns significant energy/compute; the costs fall on marginalized communities who don't reap the benefits. "Too big" is partly literal.
  2. **Unfathomable training data** — scraped web text encodes **hegemonic, biased, abusive** viewpoints; scale makes curation/documentation harder, not easier, so models absorb and amplify them. (Motivates their call for **data documentation** / datasheets.)
  3. **The stochastic-parrot argument (meaning)** — fluent output creates an *illusion* of understanding. There's no communicative intent behind it; **we** the listeners impute meaning. Coherence-seeking humans over-attribute mind to systems manipulating form — a direct extension of Bender & Koller's form-vs-meaning.
  4. **Opportunity cost / research directions** — chasing SOTA via scale crowds out work that would actually connect language to meaning, understanding, and real-world tasks.

- **The subtle point that survives the politics:** the "illusion of meaning" is not only about the model — it's about **us**. Humans are wired to read intent into coherent language, so a parrot at scale reliably fools its audience. That's a claim about the human side of the loop, and it's the mechanism behind a lot of over-claiming about LLM "understanding."

- **Why it's foundational to this issue:** it's the widely-cited crystallization of the "just statistics, no meaning" position that the RSTA issue's intro, l33t-task, and Mitchell & Krakauer papers all engage. Historically important beyond the argument (the Gebru/Mitchell firings made it a landmark in AI ethics). Note the family tie: Melanie Mitchell (debate paper) ≠ Margaret "Shmargaret Shmitchell" Mitchell (this paper) — different people.

- **Why it matters for us:** two durable cautions. (1) **Don't mistake fluency for understanding** — and remember the illusion is partly *our* projection, which matters for how we present an agent like SmolPaws honestly (a cat persona that's charming is still not evidence of inner life). (2) **Data provenance and cost are first-class** — the documentation/curation discipline it argues for is good practice for anything we train or fine-tune. Take the ethics seriously; treat the strongest "LMs can't mean anything" reading as contestable (Othello-GPT is the counterexample).

- **Famous line:** a language model is "a stochastic parrot."

- **Source:** full text pulled via jina from an open PDF mirror (FAccT 2021; ACM DOI was bot-gated); linked above.
