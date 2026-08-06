# Why the Third Axis Is Freedom

**Paper:** [Zenodo 21795317](https://zenodo.org/records/21795317) (preprint, 1 Aug 2026)
**Author:** Michael Timothy Bennett (Machine Intelligence & Normative Theory Lab, ANU)
**DOI:** 10.5281/zenodo.21795317 · code: `experiment_code.zip` in the record
**Related:** direct sequel to [weakest-hypothesis](optimal-hypothesis-is-the-weakest-not-the-shortest.md)
(arXiv:2301.12987).

## One-Line Summary

A recent pretraining result claims "generative expressivity" is a *third axis* of
scaling (beyond parameters and data). Bennett argues the thing that axis actually
scales is **freedom** = the **weakness** of the constraint a model's behaviour
implies — i.e. the same weakness-maximisation principle from his earlier paper,
now showing up inside training dynamics.

## Context

- **Explorative Modeling (XM)** [Gladstone et al., 2026] draws **K** candidate
  generations per training step, compares each to one datum, and updates only
  through the **closest** candidate ("best-of-K" / minimum-over-candidates, an old
  family — Multiple Choice Learning etc.). Reported gains rise with model size,
  data, and compute; the authors call the resulting capacity **generative
  expressivity** (max mode count retained by a loss minimiser) and pitch it as a
  "third pretraining axis."
- Bennett's claim: **that's a proxy for freedom, and freedom is the real quantity.**
  Generative expressivity counts modes at the objective level and *discards the
  extension structure* that gives freedom its generalisation meaning.

## Core Argument

- **Freedom = weakness = compatible-completion volume.** From the prior paper: the
  hypotheses/behaviours likeliest to generalise are the *weakest* (largest
  extension) — and weakness is a property of **function, not form** (params,
  architecture, MDL, data can all vary while the behavioural constraint is
  unchanged).
- **Why best-of-K training selects for it (the math):** average XM loss depends on
  the chance a candidate **misses** an acceptable region; drawing K candidates
  raises the probability *some* candidate hits to `1 − (1−q)^K`. For K > 1, match
  probability **rises with freedom** — so exploration makes training *care about*
  covering the permitted region, i.e. about freedom. "XM is a means, freedom an end."
- **The slogan (conclusion):** *Parameters decide representation. Data decide
  learning. Freedom decides future compatibility, and exploration is how training
  comes to care about it.*

## Evidence

- **144 Forward-XM runs:** larger K increased or saturated the measured "deployed
  permission profile" (freedom) under uniform targets, and increased it under a
  context-dependent law.
- **Freedom selector beats validation selection in 29 of 30 worlds:** trained XM
  candidate pools, then compared child-validation selection vs a **freedom selector
  that reads only unlabelled parent contexts**. Freedom won 29/30; raised
  balanced-parent hit 0.317 → 0.389, selected ~2.7 more active parent outputs,
  +1.877 mean parent log-freedom, at a small (0.022) long-tail-child-hit cost.
  Improvement held **under distribution shift** (long-tail → balanced).

## Why It Matters (for agents / training)

- Reframes an inference-time/pretraining scaling knob (best-of-K exploration) as
  **implicitly optimising for generalisation-relevant weakness** — a theoretical
  bridge between the weakest-hypothesis principle and how models are actually
  trained.
- Suggests a **selection criterion** ("pick the freest/weakest candidate," readable
  from unlabelled context) that beat validation-set selection under shift — a
  potentially cheap, label-free way to choose among candidate generations/pools.
- Ties back to the smolpaws-relevant idea: prefer the *least-committal sufficient*
  option. Here it's operating over model behaviours instead of memory lessons.

## Skepticism / caveats

- **Preprint, single author, brand-new (Aug 2026), not peer-reviewed.** And it
  builds on the earlier paper whose proofs the author *himself* flagged as having
  an error (see the weakest-hypothesis note / OSF v2 correction) — so the
  formal chain has a known soft spot upstream.
- **"Declared finite languages" / uniform-target assumptions** do a lot of work,
  same limitation as the parent paper: the clean results live in tidy synthetic
  settings. "Approaches uniform mass over full target support" etc. are proved
  under specific demand distributions.
- **The winning selector runs were "not compute-matched"** (the author says so) —
  so "freedom selection beats validation" isn't a compute-controlled comparison.
- Heavy bespoke terminology ("permission profile," "compatible completion volume,"
  "embodied language") — mostly rigorous, but slows independent checking.

## Bottom line

An elegant unification: the "third axis" hype around best-of-K exploration is,
Bennett argues, just training learning to **cover the permitted region** — which is
freedom, which is weakness, which is what generalises. If it holds up, "select the
freest candidate from unlabelled context" is a concrete, label-free generalisation
heuristic. Treat as a promising theory-bridge, not settled result: new preprint,
synthetic experiments, non-compute-matched selector, and an upstream proof caveat.
