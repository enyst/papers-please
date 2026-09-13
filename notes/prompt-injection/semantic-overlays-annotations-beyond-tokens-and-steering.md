---
title: "Semantic Overlays: Mitigating Prompt Injection with Annotations Beyond Tokens and Steering Vectors"
authors:
  - (see paper)
arxiv_id: "2608.23873"
arxiv_url: "https://arxiv.org/abs/2608.23873"
published: "2026-08"
source: "arXiv:2608.23873 [cs.CR]"
read_depth: "abstract-only"
mechanism: "Adds an out-of-band 'span identity' channel the model can't be tricked about: small learned adapters ('Semantic Overlays') applied at chosen prefill positions to a frozen model's residual stream, marking a span as user-input / tool-output / instructions — an annotation that tokens cannot forge."
tags:
  - prompt-injection
  - defense
  - span-identity
  - steering
  - adapters
  - representation-engineering
categories:
  - cs.CR
---

- **One-line take:** Attacks the root cause — **everything the model sees is tokens, so it must track span identity (user vs tool vs instruction) itself, and text can be written to read like anything.** Semantic Overlays add a *non-textual* channel marking each span's identity directly in the residual stream, "an out-of-band annotation that cannot be replicated by tokens." Prompt injection is, at bottom, span-identity confusion; this gives the model ground truth about it.

- **Mechanism:** small **learned adapters** applied at chosen prefill positions over a frozen model's residual stream. Unlike (untrained) steering vectors, overlays are trained/adaptable and lay over a *span* to stamp its provenance. The serving stack already knows each span's role — this pipes that knowledge into the model out-of-band.

- **Why it matters for us:** the most architecturally interesting defense of the batch — it's the representation-level answer to "the model loses track of what's instruction vs data" (cf. `prompt-injection-as-role-confusion` already in our corpus, and `interpretability/steering-vectors`). Needs model-internals access (adapters), so it's an upstream/provider-side fix, not something we bolt onto a closed model — but conceptually important. Ties prompt-injection ↔ interpretability.

- **Source:** abstract via arXiv:2608.23873 (Chrome). Not yet full-read.
