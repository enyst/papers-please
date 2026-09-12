# World Models in Natural and Artificial Intelligence

Notes on the **theme issue** *"World models in natural and artificial intelligence"* —
*Philosophical Transactions of the Royal Society A*, **Volume 384, Issue 2320** (14 May 2026).
Issue: <https://royalsocietypublishing.org/rsta/issue/384/2320>

18 primary articles (one further item in the issue is an unrelated *correction* to a
2024 packaging-films paper and is intentionally not noted here). Every article gets a
note; **11 were read in full** (the original 8, plus narrative world models, brain
inner-time, and unconventional embodiments — the latter three promoted at Engel's
request on 2026-09-12), and the remaining 7 are recorded at **abstract depth** with an
honest flag on whether they're worth a later full read.

## What the issue is about

How do natural and artificial systems **model the world**, and what does that reveal
about the relationship between life and mind? The editors deliberately refuse a single
definition of "world model" and instead survey a *family* of them — causal,
self-referential, goal-directed, collective, narrative. The spine running through every
paper: **do scale-trained AI systems acquire the context-sensitive, temporally-embedded,
value-laden, embodied kind of world-modelling that biological minds run on — or only
statistical surface regularities?** No settled verdict; it's framed as the productive
fault line.

Read `world-models-agi-life-mind-continuity.md` first — it's the editors' own map.

---

## Final list A — read in full (11)

Ranked by how much they earned the full read (most compelling first). The last three
were promoted from abstract-depth at Engel's request (2026-09-12).

1. **AI for science: the easy and hard problems** (`ai-for-science-easy-and-hard-problems.md`)
   — the "easy problem" = optimize a given objective; the **"hard problem = the problem
   problem"** = inventing/revising the problem itself. The sharpest statement of the
   concept-formation gap. *Most Engel-relevant paper in the issue.*
2. **Human-level learning of complex novel tasks (theory-based RL / EMPA)**
   (`theory-based-rl-human-level-learning.md`) — humans learn 90 games in minutes;
   structured *causal intuitive theories* as world models match that. The best
   constructive case for "world model = structured causal theory."
3. **A sentence is worth a thousand pictures (the l33t task)**
   (`a-sentence-is-worth-a-thousand-pictures-leet-task.md`) — a clean behavioural
   dissociation: humans decode `l33t` text via top-down grounded repair; LLMs struggle.
   Evidence scaling ≠ grounded understanding.
4. **Levels of analysis for large language models**
   (`levels-of-analysis-for-llms.md`) — use Marr's 3 levels + cognitive-science methods
   to understand LLMs; "embers of autoregression." The methodology paper.
5. **Empowerment gain and causal model construction**
   (`empowerment-gain-and-causal-model-construction.md`) — Gopnik: "empowerment"
   (control over outcomes) as the optimizable bridge between causal-Bayes-net learning
   and RL. An objective for agents that *want to understand*.
6. **Large language models and emergence: a complex systems perspective**
   (`llms-and-emergence-complex-systems.md`) — rigorous emergence; "More is Different"
   (capabilities) vs "Less is More" (intelligence = efficient reuse). Emergence ≠ intelligence.
7. **Unexpected benefits of self-modelling in neural systems**
   (`unexpected-benefits-of-self-modelling.md`) — predicting your own internal states as
   an auxiliary task makes a network simpler/more regularized (RLCT drops). Self-model
   as self-regularization.
8. **World models, AGI and the hard problems of life–mind continuity** (the intro)
   (`world-models-agi-life-mind-continuity.md`) — the editorial / conceptual map. Read
   first for orientation even though it's ranked last among the original 8.
9. **Brains and where else? Theories of consciousness to unconventional embodiments**
   (`theories-of-consciousness-unconventional-embodiments.md`) — Levin: a substrate audit
   of the major consciousness theories; almost nothing in them actually requires neurons,
   so continuity/"mind everywhere" is the null hypothesis. The issue's substrate-independence pole.
10. **What physics offers for AI: the brain's inner time** (`what-physics-offers-ai-brain-inner-time.md`)
    — Northoff: the brain's spontaneous, scale-free "inner time" actively entrains to the
    world; machines lack it and are "locked out of time and world." The temporality pole
    (and the direct foil to #9).
11. **Two kinds of narrative world models** (`two-kinds-of-narrative-world-models.md`)
    — Breithaupt: an "experience-focused" world model defined by *not knowing*, enabling a
    **self-update**; AI's missing ingredient is a *standpoint*/positionality. Ties to
    memory/identity revision.

## Final list B — recorded at abstract depth (7)

With a flag on whether a later full read looks worth it:

- **Revisiting Rogers' Paradox in human–AI interaction** (`rogers-paradox-human-ai-interaction.md`)
  — humans learning from AI that learns from humans; collective-world-model feedback loops.
  **Strongest full-read candidate of this group** (topical: epistemic feedback / model collapse).
- **Is there an 'I' in AI?** (`is-there-an-i-in-ai.md`) — essay on reference/meaning
  ("words that act like things mean those things"). Full-read candidate if pulling the
  meaning/reference thread.
- **Goals and the structure of experience (telic states)** (`goals-and-the-structure-of-experience-telic-states.md`)
  — descriptive + prescriptive world-model halves co-emerge from the goal; Buddhist
  epistemology. Theory, not yet implemented.
- **On the representation complexity of model-based vs model-free RL**
  (`representation-complexity-model-based-vs-model-free-rl.md`) — formal proof: model
  cheap to represent, optimal Q-function exponentially expensive. The theory companion to #2.
- **A 'good' regulator may provide a world model** (`good-regulator-world-model.md`)
  — the cybernetic Every Good Regulator Theorem recast for modern AI.
- **Topological constraints on self-organization** (`topological-constraints-on-self-organization.md`)
  — stat-mech of when local interactions sustain global order; bonus: a physics reason
  autoregressive models struggle with long sequences.
- **Cognitive glues are shared models of relative scarcities** (`cognitive-glues-economics-collective-intelligence.md`)
  — the price system as the economy's "cognitive glue"; template for all collective-mind coordination.

---

## Foundations & the LLM-understanding debate (not in the issue, but its bedrock)

Companion classics — added because every "does it *understand*?" / "is there an 'I'?" /
"is it just statistics?" argument in the issue is downstream of these. Full texts were
pulled where reachable; each note links its source. Grouped by role:

**The founding question**
- **Turing, "Computing Machinery and Intelligence" (1950)** (`turing-computing-machinery-and-intelligence.md`)
  — swaps "can machines think?" for the operational imitation game; rebuts nine
  objections; proposes the *child machine* (learning). The behavioural standard the whole
  debate contests.

**Consciousness / the "I"** (phenomenal side)
- **Nagel, "What Is It Like to Be a Bat?" (1974)** (`nagel-what-is-it-like-to-be-a-bat.md`)
  — consciousness is irreducibly *subjective*; objective description can't capture it.
- **Chalmers, "Facing Up to the Problem of Consciousness" (1995)** (`chalmers-facing-up-hard-problem.md`)
  — names the *hard problem* (why functions are accompanied by experience). Systematizes Nagel.
- **Block, "On a Confusion about a Function of Consciousness" (1995)** (`block-two-concepts-of-consciousness.md`)
  — splits *access* vs *phenomenal* consciousness — the precision tool for talking about
  machine minds without equivocating.
- **Dennett, "Real Patterns" (1991)** (`dennett-real-patterns.md`) — the deflationary
  counter-pole: a pattern is real iff it compresses the data; minds are real patterns, not
  fundamental things. Underpins "emergence" done rigorously.

**Meaning, syntax, grounding** (the "does it understand?" lineage)
- **Searle, "Minds, Brains, and Programs" — the Chinese Room (1980)** (`searle-minds-brains-and-programs-chinese-room.md`)
  — syntax isn't sufficient for semantics.
- **Harnad, "The Symbol Grounding Problem" (1990)** (`harnad-symbol-grounding-problem.md`)
  — formalizes Searle into a research problem; proposes grounding symbols bottom-up in
  perception (neurosymbolic). The load-bearing classic for the grounding thread.
- **Bender & Koller, "Climbing towards NLU" — the octopus test (2020)** (`bender-koller-climbing-towards-nlu-octopus.md`)
  — meaning can't be learned from form alone. The modern, linguistics-grade version.
- **Bender, Gebru et al., "Stochastic Parrots" (2021)** (`stochastic-parrots.md`) — the
  "illusion of meaning" (partly *our* projection) + the cost/bias critique.

**The live debate + the constructive (world-models / concept-formation) reply**
- **Mitchell & Krakauer, "The Debate Over Understanding in AI's LLMs" (2023)** (`mitchell-krakauer-debate-over-understanding.md`)
  — the best survey of the fault line (statistics vs causal mechanism); by two of this
  issue's editors. Read right after the issue intro.
- **Li et al., "Emergent World Representations" — Othello-GPT (2023)** (`othello-gpt-emergent-world-representations.md`)
  — empirical: a next-token model builds a probeable, *causally-usable* board model. The
  strongest reply to the skeptics.
- **Lake, Ullman, Tenenbaum & Gershman, "Building Machines That Learn and Think Like People" (2017)** (`lake-building-machines-that-learn-and-think-like-people.md`)
  — the manifesto behind theory-based RL: intuitive physics/psychology + compositional,
  causal, learning-to-learn model-building.
- **Lake, Salakhutdinov & Tenenbaum, "Human-level concept learning through probabilistic program induction" (2015)** (`lake-human-level-concept-learning-program-induction.md`)
  — the empirical one-shot concept-learning result (BPL / Omniglot). Concept formation as
  program synthesis. *Most on-target for Engel's concept-formation interest, with Lake 2017.*

How they line up against the issue: **Turing** sets the behavioural bar; **Searle → Harnad
→ Bender&Koller → Parrots** build the "no meaning without grounding" case (the l33t-task
paper is their empirical echo); **Othello-GPT + the two Lake papers** are the constructive
"structured/emergent world models" reply (parents of the theory-based-RL and
representation-complexity notes); **Nagel/Chalmers/Block/Dennett** frame the
consciousness/"I" axis (Nagel↔Levin, Chalmers↔Dennett as the poles).

---

## Why this issue is in the corpus (relevance to our work)

It's the philosophy-and-cognitive-science backbone for the questions SmolPaws/Engel care
about most: **concept formation** (easy vs hard problem of science), **grounding &
understanding vs statistics** (l33t task, emergence), **world models as structured causal
theories** (theory-based RL, representation complexity, empowerment), **self-models**
(self-regularization), and **methodology for understanding opaque models** (Marr levels).
It complements `notes/memory/` (a learned world model *is* a compact reusable memory) and
`notes/interpretability/` (levels of analysis).

## Method note

Table of contents + abstracts + the 11 full texts were read via the browser (the
publisher is behind Cloudflare; direct fetch/jina were blocked). Abstract text is quoted
from the article pages; the "why it matters" commentary is mine.
