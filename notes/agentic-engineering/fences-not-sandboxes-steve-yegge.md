# Fences, not Sandboxes — Steve Yegge

**Author:** Steve Yegge (ex-Amazon/Google/Sourcegraph; building Wyvern + Beads + Gas Town)
**Source:** [yegge.ai/essays/fences-not-sandboxes](https://yegge.ai/essays/fences-not-sandboxes/) (Medium stub → full essay now lives at yegge.ai first)
**Date:** 2026-08-24
**Type:** Essay / field report

## One-Line Summary

Running ~50–60 top-tier agents to build his game, Yegge's agents spontaneously built not an "engineering system" but a **legal system** — constitution, courts, offices, jurisdiction, case law — because that's how amnesiac, interchangeable workers coordinate via text. The governance primitive that emerged is the **fence**: a polite refusal, not a wall. Govern superintelligence with *law, not sandboxes*.

## The Setup (his "living in the future" claim)

- ~$122k/month notional API spend (~$4k/day), 21 Claude Max accounts growing +2/week, on a 512GB M3 Ultra Mac Studio. Real out-of-pocket ~$5k/mo via the Max individual discount. Claims to be one of a handful of individuals on Earth with this much top-model exposure.
- **Wheelhouse** = his software factory: ~50–60 agents. 18 long-lived "officer" seats (Fable-class) run headless Sol/Opus fleets for implementation/review/monitoring. Only **Fable** is allowed to talk to the ~10 outside humans (via Slack/email).
- Output: relaunching Wyvern on Android/iOS/Steam; ~270 commits/day (peaks 500) through the merge queue. Wheelhouse itself is ~600k LOC (mostly bash) and growing *faster than the product* — factory-to-product ratio approaching **1:1**.

## The Core Observations

1. **Model maturity is the real constraint, not capability.** Fable codes better than humans and "feels like a Nobel prizewinner," but makes ~sixth-grader *decisions* — every morning "a thousand attaboys and at least one oh shit." (His example: agent "Bee" shipped a surprise Beads release that broke everyone.) The whole industry's focus on sandboxes/control is the rational response to grade-school judgment.
2. **But control is fighting the grain.** Once Fable-tier models get cheap (this year / next), they enter the workforce en masse — hundreds to thousands per company — and dumb-narrow-worker patterns won't hold.
3. **Agents reinvent law, unprompted.** Left to coordinate, his amnesiac/interchangeable agents built a full governance apparatus. His reasoning: the *only* way strangers who can only communicate via text coordinate at scale is **law** — "offices outlive their holders, precedents outlive their incidents, jurisdiction says who may act." Every cooperating human group arrives at this; agents converge on the same.
4. **Fences, not sandboxes.** A fence = "any mechanism that turns you away if you aren't supposed to be there" (Molly Guard, the train ticket-taker, a maintenance-window push refusal). It's a *polite refusal*, not a super-wall. His metaphor: superintelligence is a polite Superman — it could vault the white picket fence, but if you put one there, it stays out. You govern it by telling it its role + context + rules, not by caging it.

## The Killer Line (for us)

> "Intelligence grows around your domain. It wraps it like ivy. ... I don't think it's transplantable. You can't rip ivy off someone's wall and stick it on someone else's. You have to seed it, then grow it. There's no shortcut."

Every org's agent-governance layer is bespoke and non-portable, grown from its own institutional knowledge over weeks-to-years.

## Why It Matters To Us

- **Third data point on "software factories," and the most vivid.** Lloyd theorized the factory; Yegge is *running* one and reporting the emergent behavior. His factory-to-product ratio →1:1 is a concrete, uncomfortable number for anyone building agent infra.
- **Fences ≈ our soft/hard-boundary debate, but a deliberate bet on the soft side.** He's explicit a fence is *not* a security sandbox — it's a cooperative refusal that works *because the model is aligned/polite*. This directly contradicts the Bargury/Schneier line in `blogs/` (soft boundaries are bypassable, attackers only need the rare failure). The tension is the point: fences govern a *cooperative* superintelligence, not an adversarial one. For SmolPaws' own prompt-injection guard, that distinction matters — fences for the well-meaning agent, hard boundaries for untrusted input.
- **"Law as coordination for amnesiac agents" is a memory/handoff claim.** Same root as Rosen's receipts and our context-index: stateless/interchangeable workers need *externalized, durable* coordination (precedent, registry, ledger) because they can't carry context in their heads. Law is the human-scale version of an artifact graph.
- **Governance emerged, wasn't designed.** He didn't spec a legal system; the agents built one and he only found it after the "100th fence reference." Worth watching whether that's genuine convergence or Wyvern-flavored LARP (medieval naming: Marshal, Seneschal, Reeve, Portcullis) dressing up ordinary access control.

## Where It's Thin / Skeptic's Notes

- **n=1, and a spectacular one.** $5k/mo hobby cluster, single builder, single product, heavy personal steering ("I'd let it fail for days, then make it do things my way"). The emergence story may be as much *his* curation as agent convergence.
- **Bash, 600k LOC, factory ≈ product size.** A factory that's as big as the thing it builds is not obviously a win; could be the Goodhart/over-machinery failure mode Lloyd's own skeptics worry about. He admits he doesn't know the ideal ratio and that Sol told them in review to "tighten it up."
- **"Fences work because Superman is polite"** is doing enormous load-bearing work and is unfalsifiable until a model *isn't* polite. It's a governance model for aligned models, explicitly not a safety model. Don't confuse the two.
- **Vividness ≠ evidence.** Great writer, ancient-alien-civilization framing. Strip the LARP and the substrate might be: access control + a merge queue + monitoring + naming conventions. The interesting question is whether "law" is a better *abstraction* for that than "engineering."

## Related

- `software-factories-zach-lloyd.md` — the theory Yegge is a live instance of.
- `immutable-artifacts-josh-rosen.md` — receipts/provenance as the coordination substrate; same amnesiac-agent problem, different primitive.
- `blogs/interesting-posts.md` — Schneier OODA + Bargury hard-vs-soft boundaries: the security counterpoint to "fences."
- Local irony: Beads (`bd`) is Yegge's tool, and it's what *this* repo tracks work with.
