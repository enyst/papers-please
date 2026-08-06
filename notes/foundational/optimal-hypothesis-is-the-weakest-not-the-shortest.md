# The Optimal Choice of Hypothesis Is the Weakest, Not the Shortest

**Paper:** [arXiv:2301.12987](https://arxiv.org/abs/2301.12987) (v4, Apr 2024)
**Author:** Michael Timothy Bennett (Australian National University)
**Venue:** AGI 2023 (Artificial General Intelligence)
**Appendices / proofs:** on GitHub / Zenodo (doi:10.5281/zenodo.7641742)

## One-Line Summary

To pick the hypothesis most likely to generalise, don't choose the **shortest**
(minimum description length / compression); choose the **weakest** — the one whose
"extension" (the set of things it permits) is largest, i.e. the least specific
explanation consistent with the data.

## Why it's here (the note Engel flagged)

Erik Meijer (@headinthebox) gave it a big shout-out on X (Aug 2026): *"if you have
any kind of self-improvement loop, show this paper to the model and ask it to
incorporate it."* That's the hook — it's being pitched as something to bake into
an agent's self-improvement / hypothesis-selection loop, as an alternative to the
usual "prefer the simplest/shortest program" (Solomonoff/MDL/Ockham) prior.

**Caveat the author himself added** ([@MiTiBennett reply](https://x.com/mitibennett/status/2085053682891268522)):
there is *"an error in one of the proofs and some updates to the formalism"* fixed
in a later note — the corrected version is an OSF preprint
(`osf.io/preprints/osf/qf8tw_v2`). So treat the v4 arXiv proofs as the idea, not
the final formal word; read the OSF update before leaning on the theorems.

## Core Idea

Setup: sets `A ⊂ B`. Generalisation = inferring from `A` a hypothesis sufficient
to construct `B`. Many hypotheses fit `A`; only some extend to `B`. Which to pick?

- **The usual answer:** the shortest. MDL/Kolmogorov/Solomonoff equate compression
with generalisation ("compression ≈ intelligence"), so you prefer the shortest
program that explains the data. Bennett argues this proxy "has gone unchallenged."
- **Bennett's answer — weakness.** In his enactive-cognition formalism, every
statement `l` has an **extension** `Z_l` = the set of statements it is compatible
with / that entail it. The **weakness** of `l` is `|Z_l|`, the cardinality of that
extension. A *weak* statement permits many possibilities; a *strong* one nails
things down. Claim: pick the **weakest valid hypothesis**.

**The theorem (informal):** if tasks are uniformly distributed, the number of tasks
a statement `l` generalises to is `2^|Z_l|` — so maximising weakness is *necessary
and sufficient* to maximise the probability that induction yields a hypothesis that
generalises. No other proxy can do at least as well as weakness-maximisation on all
tasks while beating it on any. Minimum description length is shown to be **neither
necessary nor sufficient**.

## Weakness ≠ Ockham's Razor

The key subtlety. Weakness is about **extension (meaning), not form (length)**:
- A *short/simple* statement can be **strong** (over-specific): "all things are blue
crabs" is short but permits almost nothing.
- A *long/complex* statement can assert almost nothing (be weak).

So this is not "prefer simple." Bennett proposes a different razor —
**"Bennett's Razor": *Explanations should be no more specific than necessary.***

## Evidence

Experiments on **binary arithmetic** (propositional-logic tasks, `|D_k|` = 4–14
examples per trial): maximising weakness generalised at **1.1× to 5×** the rate of
minimum description length. He also argues weakness explains why DeepMind's
**Apperception Engine** (Evans et al., a Kant-inspired inference engine) generalises
well — it implicitly favours weak hypotheses.

## Why It Matters (for agents / self-improvement)

- Offers a **selection criterion for hypotheses/rules** that is provably (modulo the
noted proof fix) better than "shortest," under the uniform-task assumption. For an
agent that induces rules about its environment or itself, "keep the least-committal
rule that still fits" is an actionable heuristic distinct from "keep the simplest."
- Challenges the compression=intelligence equation that underlies a lot of AGI
theory (Hutter/AIXI, Legg-Veness, Chollet's ARC framing).
- Open problem the author names: **how to maximise weakness inside neural nets** —
it's clean in a symbolic/logic setting; the NN operationalisation is unsolved.

## Skepticism / caveats

- **Author-acknowledged proof error** (see OSF v2). Don't cite the v4 theorems
without checking the correction.
- **"Uniform distribution over tasks"** is doing heavy lifting — the necessity/
sufficiency result is conditioned on it. Real task distributions aren't uniform
(that's the whole basis for simplicity priors working in practice), so "weakest
beats shortest" in general is not established outside that assumption.
- **Weakness must be "well defined"** in the language — assumes a formalism where
extensions are enumerable/measurable; the binary-arithmetic experiments live in
exactly such a tidy symbolic setting.
- Practicality for LLMs is aspirational: Meijer's "show it to your model" framing is
a vibe, not a method. There's no NN recipe here yet.

## Relation to other work

Against MDL/Solomonoff/Kolmogorov compression priors and Chollet's *On the Measure
of Intelligence*. Builds on Bennett's own enactive-cognition line ("Symbol Emergence
and the Solutions to Any Task," "Computational Dualism") and formalises intuitions
behind DeepMind's Apperception Engine (Evans' formalisation of Kant).

## Follow-up

Bennett's sequel — [Why the Third Axis Is Freedom](why-the-third-axis-is-freedom.md)
(Zenodo 21795317, Aug 2026) — applies this "weakness = freedom" idea to *pretraining*,
arguing best-of-K "Explorative Modeling" implicitly optimises for freedom (weakness),
and that a freedom selector reading unlabelled context beats validation selection
under distribution shift (29/30 worlds).

## Operational companion

There's a skill that turns this principle into an agent procedure —
[`Umaraslam66/ml-superpowers` → `skills/weakest-hypothesis`](https://github.com/Umaraslam66/ml-superpowers/blob/main/skills/weakest-hypothesis/SKILL.md)
(MIT). It reframes the idea as: enumerate candidates → discard insufficient →
adopt the weakest sufficient (delete any attribute that still explains
everything) → state what's open. Adopted into smolpaws at
`.agents/skills/weakest-hypothesis/`. Directly useful for reflection / lesson
encoding (scope a memory to the weakest sufficient explanation, not the
incident) and for diagnosing from a few failure reports.

## Bottom line

A genuinely interesting reframing: **generalisation power comes from a hypothesis
being *permissive* (weak), not *short* (simple)** — and short ≠ weak. Worth knowing
as a selection principle for rule-inducing / self-improving agents. But: read the
OSF-corrected version for the proofs, and remember the headline theorem rides on a
uniform-task assumption that doesn't hold in the wild.
