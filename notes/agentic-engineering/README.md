# Agentic Engineering

Ideas, from everywhere, on how to *engineer* with coding agents — not just prompt them. The shift is from one-shot vibe coding toward treating agent-driven software work as a real engineering discipline: measurable, version-controlled, verifiable, improvable over time.

This directory collects primary sources (tweets, blogs, papers, vendor manifestos) and pulls out the durable idea, the sharp claim, and where it argues with the others. Marketing gets stripped; the mechanism stays.

## The through-line

Two questions keep recurring across everything here:

1. **How do you improve the loop, not just the output?** Move the unit of engineering up a level — from "the diff the agent produced" to "the system that produces diffs." Measure it, version it, let agents propose changes to it.
2. **How do you trust the output without watching every step?** Instead of a human re-checking each action, demand durable, verifiable evidence of what the agent relied on and did — receipts, immutable artifacts, provenance graphs.

The first is about *self-improvement*; the second is about *verifiability*. They meet at the same place: you can grant an agent more autonomy exactly to the degree that the system around it produces trustworthy, inspectable state.

## Sources

| File | Author | Core claim |
|------|--------|------------|
| [`software-factories-zach-lloyd.md`](./software-factories-zach-lloyd.md) | Zach Lloyd (Warp) | Deploy coding agents with an engineering mindset: a cloud "software factory" — SDLC automation loops defined as code, measured against your own data, self-improving via scorer + improvement agents. |
| [`immutable-artifacts-josh-rosen.md`](./immutable-artifacts-josh-rosen.md) | Josh Rosen | Trust agents with consequential work by making them leave *receipts*: immutable artifacts that reference the exact upstream artifacts they used, forming a provenance graph of the work. |
| [`fences-not-sandboxes-steve-yegge.md`](./fences-not-sandboxes-steve-yegge.md) | Steve Yegge | Field report from a live ~50-agent "software factory": the agents spontaneously built a *legal system* to coordinate. Govern superintelligence with *fences* (polite refusals) and law, not sandboxes. |

## Open threads to chew on

- **Factory vs. receipts are complementary, not rival.** Lloyd optimizes the *loop*; Rosen hardens the *evidence*. A factory that emits immutable artifacts is stronger than either alone — the scorer agents in Lloyd's loop would grade Rosen's receipts.
- **Who defines the scoring dimensions?** Lloyd's self-improvement hinges on humans defining "cost, quality, verbosity" and reviewing PRs against the factory definition. That's the real bottleneck, and it's underspecified.
- **Provenance is also a security surface.** An immutable work graph is close to the dataflow-integrity argument (see `notes/prompt-injection/` and Schneier's OODA post in `blogs/`). Receipts help audit *after*; they don't stop a poisoned upstream artifact from propagating.
- **Vendor gravity.** Most come with a product attached (Warp; Rosen's framing maps onto artifact/graph platforms; Yegge sells the field report as consulting). Note the idea separately from the pitch.
- **Law vs. sandboxes (Yegge) sharpens question 2.** Lloyd/Rosen make work *inspectable*; Yegge argues you then govern it with *fences* — polite refusals that work because the model is cooperative — not walls. That's a live bet against the hard-boundary/dataflow-integrity camp, and only holds while models stay "polite." Fences for cooperative agents, hard boundaries for untrusted input.
- **Factory-to-product ratio.** Yegge's Wheelhouse is approaching 1:1 with the product it builds. Is that the cost of doing it right, or Lloyd's own Goodhart/over-machinery risk made concrete? Open.
- **Amnesiac coordination is the shared root.** Rosen's receipts and Yegge's "law" are two answers to the same problem: interchangeable, context-less agents need *externalized durable state* (provenance graph / precedent + registry) to cooperate. Same family as our context-index and `handoff` skill.

## Related in this repo

- `notes/harness/` — the harness *is* the factory's runtime; code-as-harness and the Harness Handbook are the low-level view of what Lloyd calls the factory definition.
- `notes/memory/` — Rosen's "another agent continues without inheriting context" is a memory/handoff claim; the artifact graph is an external-memory design.
- `notes/skills/` — self-improving factories that propose diffs to their own definition ≈ skill discovery/optimization at the workflow level.
- `blogs/interesting-posts.md` — Schneier OODA, dataflow-controls security, prompts-as-code all touch these themes.
