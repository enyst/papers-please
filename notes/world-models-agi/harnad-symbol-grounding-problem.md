---
title: "The Symbol Grounding Problem"
authors:
  - Stevan Harnad
doi: "10.1016/0167-2789(90)90087-6"
url: "https://arxiv.org/abs/cs/9906002"
source_pdf: "https://www.cs.ox.ac.uk/activities/ieg/e-library/sources/harnad90_sgproblem.pdf"
published: "1990"
source: "Physica D, Vol. 42 (1990), pp. 335–346"
article_type: "Classic cognitive-science paper"
read_depth: "full (pulled full text)"
mechanism: "Names and formalizes the symbol grounding problem: how a formal symbol system's tokens get *intrinsic* meaning rather than meaning parasitic on interpreters' heads. Proposes a bottom-up hybrid: symbols grounded in iconic + categorical (learned feature-detector) nonsymbolic representations."
tags:
  - symbol-grounding
  - meaning
  - intentionality
  - neurosymbolic
  - categorical-perception
  - connectionism
  - chinese-room
  - classic
categories:
  - artificial intelligence
---

- **One-line take:** The paper that turned Searle's intuition into a *research problem*. **The symbol grounding problem:** how can the meanings of symbols be **intrinsic** to a system rather than "parasitic on the meanings in our heads"? Manipulating meaningless tokens by their shapes can only ever yield more meaningless tokens — "like trying to learn Chinese from a Chinese/Chinese dictionary alone." This is the load-bearing classic behind the entire grounding thread of the RSTA issue.

- **The problem, precisely:** a pure symbol system (syntax over arbitrary token shapes) has no way to connect its symbols to what they're *about*. Interpreting them requires an outside mind. So symbolic AI's "meaning" is borrowed, not owned. (Note the explicit tie to Searle: the Chinese-dictionary image *is* the Chinese Room, recast as a representational question rather than a thought experiment.)

- **Harnad's proposed solution — a bottom-up hybrid (this is the constructive part):**
  1. **Iconic representations** — analog transforms of the sensory projections of objects/events (raw perceptual shadows).
  2. **Categorical representations** — learned (and some innate) **feature-detectors** that pick out the invariant features distinguishing categories from their sensory projections.
  3. **Symbolic representations** — elementary symbols are the *names* of those grounded categories; higher-order symbols are strings composing them ("an X is a Y that is Z"). Meaning flows **up** from grounded categories, not sideways between symbols.
  - **Connectionism's role:** the natural mechanism for learning the invariant feature-detectors — so Harnad's answer is explicitly **neurosymbolic** (symbols grounded by neural-net perception), decades before the term was fashionable.

- **Why it's foundational to this issue:** it's the missing middle between Searle (1980) and the modern papers. The RSTA **l33t-task** paper ("models rely on fixed word↔vector associations, lacking grounded cognition") is a direct empirical test of ungroundedness; **Bender & Koller's octopus** is the same argument for language specifically; **"Is there an 'I' in AI?"** ("when words act like things, they mean them") is a grounding-by-use rejoinder. Harnad frames the axis all of them sit on.

- **Why it matters for us:** it names precisely what an agent needs to *mean* its symbols rather than shuffle them — grounding in sensorimotor/categorical structure. For a text-only LLM agent it's the sharpest statement of what's structurally missing, and it predicts the fix isn't scale but *grounding channels* (perception, action, causal interaction — cf. empowerment and theory-based RL in this issue). The honest counterweight: Othello-GPT suggests token-only training can induce *some* internal world structure, complicating the strict "no grounding without sensors" line.

- **Famous line:** the meanings must be made "intrinsic to the system, rather than just parasitic on the meanings in our heads."

- **Source:** full text pulled via jina from Harnad's arXiv/eprint HTML (Physica D 1990); linked above.
