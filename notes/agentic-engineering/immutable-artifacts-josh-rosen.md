# Show Me the Receipts — Immutable Artifacts for Agent Work

**Author:** Josh Rosen ([@JoshARosen](https://x.com/josharosen))
**Source:** [x.com/josharosen/status/2093364211837493358](https://x.com/josharosen/status/2093364211837493358)
**Date:** 2026-08-28
**Type:** Essay-thread

## One-Line Summary

We don't trust agents with consequential work because we have weak evidence of what they relied on and did. Fix it by making agents leave **receipts**: immutable artifacts that reference the exact upstream artifacts used, forming a provenance graph of the work — the audit trail exists *because* the agent had to build it while working.

## The Problem

We're fine letting agents draft, summarize, research, suggest. We balk when they move money, approve actions, change core data, or carry work forward unchecked. Even for a good result, we usually can't tell what it relied on, which intermediate steps happened, whether an important step was skipped, or how another agent could safely continue. So we put a human back in the loop — and that's the ceiling on autonomy.

## The Mechanism

**Receipts = downstream artifacts that carry explicit references to the exact upstream artifacts in hand when they were created.** Not vague citations in prose — actual IDs, keys, hashes, or foreign-key-style relationships.

Example: an account-risk assessment built from a customer snapshot + usage analysis + support summary + prior risk signals should *contain references to those exact artifacts*, not just mention them. Because the upstream artifacts are **immutable**, you can retrieve the precise versions later. If the usage analysis later changes, the original assessment still points to the version that existed at the time. That is the receipt.

### The receipts form a graph

Artifacts referencing artifacts = a **work graph**. An agent might make dozens of model calls and hundreds of tool calls to produce five artifacts worth keeping; the graph records the work worth keeping. Recommendation → depends on assessment → depends on evidence + hypothesis → derived from source data. A later review references the recommendation; a revised assessment references both the previous assessment and the new evidence that changed it.

> **Logs/traces answer a different question.** A trace tells you what the agent *did*. The work graph tells you what it *established* and what that was based on. For consequential work, the latter is what we actually want.

## Two Side Effects (arguably the real payoff)

1. **Continuation & collaboration without shared context.** Another agent doesn't need to inherit the original's whole context window. It inspects the current investigation, sees gathered evidence, reads the latest assessment, notices a superseded hypothesis, and continues. Handoffs happen *through artifacts*. Agents can also query for pending work — the model is useful forward-looking, not just backward.
2. **Governance for free.** Which policy version was referenced? Did a human review? Did new evidence change the conclusion? All preserved in the same graph. And it's **traversable in reverse**: if an upstream artifact is later found wrong, you can find every assessment and recommendation that depended on it.

## The Trust Argument (the thesis)

> "We can give an agent more freedom when we have stronger guarantees about the work it leaves behind... If we want agents to take on more responsibility, we need systems that let us verify the work without watching every step they take. When an agent says the work is finished, ask to see the receipts."

Autonomy is *purchased with verifiable evidence*. The audit trail isn't reconstructed after something breaks — it's a byproduct of doing the work correctly.

## Why It Matters To Us

- **Directly our memory/handoff problem.** "Another agent continues without inheriting the entire context" is the SmolPaws `handoff` skill and dreaming/context-index work, stated as an artifact-graph. The context-index principle ("index, don't copy") is a lightweight receipt: a pointer to the immutable source.
- **Immutability + reverse-traversal is a real design.** If an upstream fact is later found wrong, walk the graph to find everything downstream that trusted it. That's a concrete answer to "how does an agent revise beliefs" that our memory notes keep circling.
- **Complements Lloyd's factory.** A factory (Lloyd) that emits receipts (Rosen) is measurable *and* auditable. Scorer agents could grade the receipt graph directly.

## Where It's Thin / Skeptic's Notes

- **Receipts audit the past; they don't validate the present.** The graph faithfully records that an assessment used usage-analysis-v3. It says nothing about whether v3 was *correct* or whether the agent's reasoning over it was sound. Provenance ≠ correctness.
- **Poisoned-upstream propagation.** If an upstream artifact is compromised (prompt injection into source data), immutability means the graph *faithfully records the compromised chain*. Good for forensics after; not a defense. Ties to `notes/prompt-injection/` and dataflow-integrity (Schneier OODA, Bargury hard-vs-soft boundaries in `blogs/`).
- **Cost of "worth keeping."** Someone/something decides which of hundreds of tool calls become durable artifacts. Get that wrong and the graph is either bloated or missing the load-bearing step. Same curation problem as memory consolidation.

## Related

- `software-factories-zach-lloyd.md` — the loop that would produce and grade these receipts.
- `notes/memory/` — external-memory / handoff architectures; consolidation-as-curation.
- `notes/prompt-injection/` + `blogs/interesting-posts.md` — why provenance is necessary but not sufficient for trust.
