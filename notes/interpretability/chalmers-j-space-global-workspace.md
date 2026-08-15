---
title: "Is the Jacobian Space a Global Workspace? — Chalmers on Gurnee et al.'s J-space, access consciousness, and interpretability"
authors:
  - David J. Chalmers
type: "paper-note"
project: "interpretability"
scope_note: "core include"
source: "PhilPapers"
philpapers_id: "CHAITJ-2"
philpapers_url: "https://philpapers.org/rec/CHAITJ-2"
pdf_url: "https://philpapers.org/archive/CHAITJ-2.pdf"
pdf_local: "pdfs/CHAITJ-2-chalmers-jacobian-space-global-workspace.pdf"
announced: "2026-08-14"
announcement_url: "https://x.com/davidchalmers42/status/2088266230591291535"
published: "2026"
responds_to:
  - "Gurnee et al. 2026, 'Verbalizable Representations Form a Global Workspace in Language Models', Transformer Circuits Thread, 2026-07-06, https://transformer-circuits.pub/2026/workspace/index.html"
tags:
  - interpretability
  - philosophy-of-mind
  - consciousness
  - access-consciousness
  - global-workspace-theory
  - anthropic
  - transformer-circuits
  - j-space
  - jacobian-lens
  - logit-lens
  - verbalizability
  - llm-introspection
mechanism: "An analytic critique of Gurnee et al.'s claim that the J-space (Jacobian space) — a verbalizability-defined subspace of LLM activations — is a global workspace and a mechanism of access consciousness. Chalmers separates the two claims and argues the workspace evidence is weak and the access-consciousness link is only via a weak, first-order notion."
one_line_take: "The Jacobian lens is a real interpretability advance, but Chalmers argues the J-space is at best 'access-like' (not distinctively workspace-like), influences outputs rather than broadcasting, and rides on verbalizability — which is only weakly tied to genuine (higher-order) access consciousness."
key_terms:
  - "J-space / Jacobian space: subspace of activations especially apt to influence output tokens (verbalizable)"
  - "J-lens / Jacobian lens: refinement of the logit lens using a Jacobian to correct coordinate shifts across layers"
  - "access consciousness (Block): availability for report, reasoning, and control"
  - "global workspace (Baars/Dehaene): dedicated hub that broadcasts to specialized modules via recurrence + ignition"
---

# Is the Jacobian Space a Global Workspace?

David Chalmers responds to **Gurnee et al. (2026), "Verbalizable Representations Form a Global
Workspace in Language Models"** (Transformer Circuits Thread, July 6 2026 — an
Anthropic-lineage interpretability paper; Gurnee, Sofroniew, Pearce, … Jack Lindsey). Gurnee
et al. define the **J-space** ("J" = **Jacobian**, *not* judgment): a subspace of a language
model's activations whose vectors are especially apt to influence the model's output tokens —
i.e. *verbalizable* representations. They argue the J-space (a) **functions as a mechanism for
access consciousness** and (b) **closely resembles the global workspace** of Baars/Dehaene.

Chalmers' verdict: the J-space is **interesting and powerful**, but its connections to the
global workspace and to access consciousness are **overstated**. On the workspace side, most
of the evidence that the J-space is "workspace-like" is really evidence that it is
*access-like*. On the access side, the J-space rides on **verbalizability**, which is only
**weakly** tied to access consciousness in the usual sense — so the case for *robust* access
consciousness (and, downstream, for phenomenal consciousness) is weaker than advertised.

> Grounded in the full Chalmers PDF (`philpapers.org/archive/CHAITJ-2.pdf`, fetched via the
> browser once past the Cloudflare gate) **and** the primary paper it responds to (below).
> Note the deliberately measured register: this is not a "no consciousness here" polemic; it
> is a boundary-drawing exercise about *which* claim the evidence actually licenses.

## The paper it responds to (primary source)

**Gurnee, Sofroniew, Pearce, Piotrowski, Kauvar, Chen, Soligo, Bogdan, Ong, Wang, Thompson,
Abrahams, Kantamneni, Ameisen, Batson & Lindsey (2026), "Verbalizable Representations Form a
Global Workspace in Language Models,"** Transformer Circuits Thread, 2026-07-06
(<https://transformer-circuits.pub/2026/workspace/index.html>). In the paper's own words, the
**Jacobian lens (J-lens)** is "a new interpretability technique … designed to identify internal
representations that are readily available for verbal report. For each token in the model's
vocabulary, the Jacobian lens identifies a vector representation that encodes the potential for
the model to verbalize that token in the future" — computed as, per layer, "the average
linearized effect of an activation on the model's likelihood of producing a particular token
(now or in the future), averaging over a large corpus of contexts." The **averaging** is load-
bearing (it's what Chalmers later flags as a context-average vs. context-specific mismatch with
access consciousness). The paper tests **five functional properties of a global workspace** and
reports ignition-*like* onset effects (the ambiguous-input α-sweep experiment). Chalmers'
critique targets exactly this framing.

## Background — the two things being conflated

You need two pieces of theory to feel the argument.

**The lens.** The **logit lens** (Nostalgebraist 2020) applies a transformer's final
unembedding matrix to *earlier* layers, reading off, for any intermediate activation, a score
per output token (ask "what is 2+3?" and "5" lights up in later layers). The **Jacobian lens**
refines this: it applies a mathematical **Jacobian** to correct for coordinate-system shifts
between intermediate and final layers, giving a sharper map from a hidden vector to the tokens
it is apt to influence. The **J-space** is the subspace those J-lens vectors span — so a
J-space vector is, by construction, one whose activity is *especially likely to be verbalized*
in the output. (Chalmers notes the logit lens already does much of this, if less well — a fact
that will matter for the "is it privileged?" question.)

**The theory.** **Access consciousness** (Block): a state is access-conscious if it is
*available* for report, for flexible/deliberate reasoning, and for the control of action.
Contrast **phenomenal consciousness** (what it is *like*); Chalmers keeps the main focus on
access. **Global Workspace Theory** (Baars 1988; Dehaene 2014) is *one* computational theory
*of* access consciousness — not a synonym for it. Its distinctive commitments go well beyond
"available for use": a global workspace is **(1) a dedicated system that (2) broadcasts to (3)
specialized unconscious modules via (4) recurrent loops, while (5) integrating from those
modules, with (6) selective/competitive entry and (7) ignition** (all-or-none amplification on
entry). The whole force of Chalmers' Part I is that Gurnee et al.'s evidence bears on the
*generic access* properties, not on these *distinctive workspace* ones.

## Part I — Is the J-space a global workspace?

**1. The "workspace-like" properties are properties of access, not of GWT.** Gurnee et al.
themselves define their five "workspace-like" properties (verbal report, directed modulation,
internal reasoning, flexible generalization, selectivity) as *mirroring the properties of
conscious access*. So — surprisingly given the label — none of the five is a *distinctive*
workspace property. Chalmers' fix: rename them **"access-like."** Do that consistently and the
paper's core result becomes "the J-space is access-like," not "workspace-like." (He notes
Butlin et al. 2026's commentary reaches a related conclusion.) Gurnee et al. in fact concede
they don't reproduce the full GWT architecture (encapsulated competing modules, recurrent
broadcast, sharp ignition) — which *are* the distinctive properties — so the workspace claim is
already weaker than the title suggests.

**2. The J-space is not a (causal, dedicated, privileged, unified) system.** A classical
workspace is an *architectural component dedicated to* broadcast/integration and serving as the
*primary* such mechanism (Baars' "blackboard"; Dehaene–Naccache's specific long-range pyramidal
population). The J-space isn't clearly that. The deeper problem is **privilege**: Gurnee et
al.'s striking results mostly show J-space vectors beat *non*-J-space vectors — but that's
consistent with there being many other "K-spaces" whose vectors are equally superior to their
complements. A recent **R-lens** (Blank et al. 2026) reportedly works *better* than the J-lens
on earlier layers; ablation-style effects likely apply to it too. Beating five other populations
(Gurnee et al. §4.3) isn't beating *all* of them. Absent evidence that the J-space is superior
*overall*, the honest reading is: **the J-lens is a useful interpretability tool that need not
correspond to a privileged mechanism.** Chalmers frames the upshot as a **minimal-vs-substantial
workspace** spectrum — evidence for a *substantial* workspace is currently weak.

**3. The J-space supports only a limited form of broadcast — better called *influence*.**
Broadcast = one sender → many receivers simultaneously. The J-space's direct influence in a
layer reaches only the *next* layer; its crucial influence is on the *final* layer and outputs.
It doesn't fan out in parallel to many distributed modules. This is **influence**, not
broadcast — closer to **Dennett's "fame in the brain"** (and his 1978 model grounding
consciousness in effects on a *speech* module) than to Baars/Dehaene global broadcast.
Output-influence models are a legitimate class, but they are *not* global-workspace models.

**4. The J-space lacks the other GWT features — modules, recurrence, and (mostly) the rest.**
Point by point, per Gurnee et al.'s own words:
- **Modules:** "We do not provide evidence that non-J-space processing consists of
  encapsulated modules."
- **Recurrence:** their broadcast happens "over the course of the model's depth," *not* via
  recurrent connections — a standard transformer is near-entirely feedforward. That's an
  *alternative* to the GWT architecture, not an instance of it.
- **Integration:** present in some sense, but maybe not as a *privileged* mechanism (same
  caveat as broadcast).
- **Capacity limit:** yes — sparse combinations of ~25 J-lens vectors give a built-in limit
  (higher than the classic human workspace estimate).
- **Ignition:** only "ignition-*like*" degreed effects across layers, not the all-or-none
  transition of standard ignition models — leading Dehaene & Naccache (2026) to say "ignition
  remains to be fully demonstrated."

Net: at best limited integration/capacity/ignition, and **no** recurrence or modules — several
defining GWT features missing.

## Part II — Is the J-space a mechanism of access consciousness?

The engine here is the identification of the J-space with **verbalizability** (distinctive
effects on verbal outputs). Chalmers argues verbalizability and access consciousness come apart
in *both* directions.

**5. Many access-conscious contents are not verbalizable.** Novel tastes/shapes, psychedelic or
spiritual experiences, and "unsymbolized thinking" (Hurlburt & Akhter 2008) are access-conscious
(reportable-about, reasoned-about) yet resist being put into words beyond "there's that smell
again." Gurnee et al. reply that *pure* language models may differ (their only I/O is verbal
tokens) — but that (a) restricts the thesis to pure LMs, excluding multimodal ones, and (b)
still fails for concepts spanning multiple tokens (e.g. *blackmail*), which won't show in the
J-lens. A footnote sharpens this: **J-verbalizability is a context-*average*, whereas access
consciousness is context-specific and trigger-relative-dispositional** — so many representations
are access-conscious but not J-verbalizable.

**6. What matters may be effects on outputs *in general*, not verbal outputs.** In a pure LM,
verbalizability (influence on verbal tokens) roughly *coincides* with **"outputability"**
(influence on outputs at all), because outputs just are tokens. So the J-space's special
properties might track output-influence, not verbalization per se. **Testable:** run J-space
experiments on a *multimodal* model (GPT-4o, video/robotic-action models) with non-verbal
outputs. If the effects persist, the phenomenon is about outputs generally — and the paper's
"verbalizable" framing (and title) would need to change.

**7. Many verbalizable representations are not access conscious.** The converse gap. A Freudian
case: unconscious thoughts about one's mother that systematically make one say "mother" are
*verbalizable* in Gurnee et al.'s sense (they'd show in the J-space) but are **not**
access-conscious — hence not workspace contents. Verbalizability *over*-counts.

**8. Verbalizability ≠ reportability.** Gurnee et al. name *reportability* as a key criterion
of access, then slide to *verbalizability* as if interchangeable. They aren't: the Freud
patient's thoughts are verbalizable but not reportable (he can't report thinking of his mother);
conversely, an ineffable experience is reportable ("that smell again") but not verbalizable.
The crux: **reportability needs some potential *metacognitive awareness* of the state;
verbalizability needs only verbal *expression* of it.** The J-space delivers a version of
verbalizability, but not clearly genuine reportability.

This licenses a **first-order vs higher-order access** distinction. A defender can retreat to
"the J-space is at least a *first-order* workspace" (no essential role for metacognition) — but
that's a weaker claim with weaker resemblance to human consciousness. Chalmers presses that, in
metacognitively-capable humans, **first-order access *without* higher-order access looks more
like paradigmatic *unconscious* cognition** than conscious cognition.

## The phenomenal-consciousness upshot

Gurnee et al. disclaim phenomenal-consciousness implications, but many treat GWT or access
consciousness as a guide to it. Chalmers walks the chain and finds it weak at every link:

- If GWT ⇒ phenomenal consciousness (phenomenal GWT), the evidence still needs the J-space to
  *be* a global workspace — which Part I says is weak. So: weak evidence of phenomenal
  consciousness.
- If instead access ⇒ phenomenal consciousness, Part II says the J-space supports at best a
  *first-order* access — and **higher-order** access (dispositions to subjective reports like
  "I am experiencing a red square") is the better guide to phenomenal consciousness.
- **The one real route**: show the J-space supports *higher-order* introspective awareness. A
  related Anthropic study (**Lindsey 2025, "Emergent Introspective Awareness in LLMs"**) gestures
  at LLM introspection, but it's unclear this is the phenomenology-relevant kind. Worth
  investigating — not yet shown.

## Overall

Chalmers' measured bottom line: **the Jacobian lens is a genuine interpretability advance and
the J-space is a real, powerful object — but** (i) it is *access-like*, not distinctively
*workspace-like*; (ii) it **influences** outputs rather than **broadcasting**, and lacks
modules/recurrence/sharp-ignition; and (iii) it rides on **verbalizability**, which is only
weakly and non-metacognitively tied to access consciousness. So the strong readings — "a global
workspace," "the mechanism of access consciousness," and a fortiori "evidence of phenomenal
consciousness" — are **overstated**.

## Why it's here

Two threads meet. **Interpretability:** the J-lens sits squarely in the logit-lens →
readable-directions lineage (Transformer Circuits). **Philosophy of interpretability:** the
paper is a clinic in *not over-reading an interpretability artifact into a
causal-functional-mechanistic claim.* The recurring move Chalmers blocks — "vectors in space X
beat vectors outside X, therefore X is *the* privileged mechanism" — is exactly the inference an
interpretability practitioner must resist: a probe/direction that **tracks** a computation is not
thereby the computation. The "many K-spaces / R-lens beats J-lens" objection is the transferable
lesson for anyone reading features or steering vectors and tempted to call them *the* mechanism.

## Related in this repo

- `notes/interpretability/steering-vectors-and-activation-engineering.md` — the readable-directions / control lineage the J-lens extends.
- `notes/interpretability/README.md` — the circuits thread (logit lens → superposition → monosemanticity → circuit tracing).
