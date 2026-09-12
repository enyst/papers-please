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
