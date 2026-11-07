---
title: "Jev makes judgments, code makes decisions"
authors: [Allie Laabs]
published: "2026-11-03"
source: "TypeSafe AI blog, with official implementation documentation"
url: "https://typesafe.ai/blog/dont-call-it-a-decision-model"
read_depth: full
scope_note: "Full blog body/code, building guide, confidence, state, models, model-jaggedness, fan-out, companion-Noul and probability/confidence routing pages. Selected request/response and interpretation sections of Noul, Choice and Score pages. Diagrams not visually inspected; no SDK or paid API calls executed."
mechanism: "Ask Jev narrow typed semantic questions, then compose their probabilities with deterministic facts, explicit policy and approval gates in code."
tags: [jev, system-one, atomic-judgments, control-flow, confidence, calibration, evaluation]
---

**One-line take:** Design the workflow in code; use Jev for small semantic judgments inside it, and retain the judgment values, facts and rule path so each outcome can be inspected and evaluated.

## The article's architectural point

- **TypeSafe calls Jev a “System One” model:** fast, focused judgments in Kahneman's sense. The practical contribution is a decomposition method, rather than a measured new architecture or benchmark result in this post.
- Start with one real workflow. Mark the **lookups, arithmetic, boolean conditions and priority order** your software can compute. Put a narrow question beside each remaining semantic judgment. Many failures of a large “what should happen?” Choice can be avoided by making the underlying policy explicit and testable.
- Support example: Jev judges **wants money back**, **reports an unauthorized charge**, **requests a human**, **threatens legal action**, **wants to cancel**, and **is open to an offer**. Code reads eligibility, already-refunded status, amount and subscription status from authoritative records.
- Code then applies ordered branches: unauthorized-charge report → fraud workflow; person/legal request → human workflow; refund request + eligibility + amount threshold → immediate-refund preparation or refund review; eligible cancellation + openness → retention offer; otherwise continue. Those are **workflow selections**; authorization, user confirmation and execution remain separate controls.
- The example logs every semantic probability, exact fact and selected rule. A wrong route can be investigated as a **judgment error, fact error or policy/composition error**, rather than a single opaque action label.
- Adding a “waive the fee” branch adds its relevant judgment/fact and routing rule while retaining existing question definitions. TypeSafe says questions are evaluated independently. This is **evaluation isolation**, not proof of statistically independent errors or immunity to changes in shared state/model/policy. Regression-test the complete pipeline after extensions.

## Choosing the primitive

| Need | Jev result | How code reads it |
|---|---|---|
| One yes/no proposition | `Noul`: `noul = P(yes)` | Separate yes, no and review bands |
| One option among named alternatives | `Choice`: selected option, distribution, native confidence | Check applicability and chosen-option probability |
| Degree on a described ordered rubric | `Score`: expected level, level distribution, native confidence | Inspect uncertainty and probability mass across action boundaries |

- **Noul measures belief in a proposition.** A .6 answer to “is this severe?” represents uncertainty about that statement; it is not “60% severity.” For graded severity, supply descriptive Score levels.
- **Choice selects within the supplied set.** Add an applicability Noul when no option may fit. The official companion-Noul example has an out-of-catalog desk lamp classified as `desk_pro` at .96, while applicability is .02. Code uses the classification only after applicability passes. For multiple applicable labels, ask one Noul per label.
- **Score is an ordinal rubric expectation:** `score = Σ(level_index × probability)`. A mean can conceal probability on both sides of a consequential boundary. If escalation depends on levels 3–4, inspect `P(3)+P(4)` rather than the mean alone. Level spacing comes from the rubric indices; it does not recover an exact numerical quantity from prose.
- Supply clear, direct instructions and explicit true/false or contrastive criteria. Question IDs are response keys and **are not shown to the model**; put meaning in the instruction. Choice option names **are** visible. Structured instructions/criteria can hold named examples and comparison records without constructing a long prose policy.

## Probability, native confidence and the paper's gate

- The current [confidence documentation](https://docs.typesafe.ai/confidence) publishes the native formulas. They summarize the answer's own distribution; empirical correctness/calibration still needs local labels.
- **Noul:** no separate native `confidence` field. The probability itself carries the yes/no uncertainty. If needed, a derived concentration statistic is `abs(2*p - 1)`.
- **Choice, n options:** `confidence = (p_max - 1/n) / (1 - 1/n)`. For two options, native confidence **.9 means p_max .95**; **p_max .9 means native confidence .8**. Applying the same numeric threshold to both changes coverage. With fixed n, the two are monotonic transforms; thresholding both supplies no additional evidence. Changing the option set changes this mapping.
- **Score:** with most-likely level m, native confidence is `max(0, 1 - Σ p_i*abs(i-m) / MAD_uniform)`, where `MAD_uniform = mean(abs(i-(n-1)/2))`. It reflects ordinal spread around the peak. Probability near an action boundary still needs direct inspection.
- Our [JEV-as-a-Judge note](jev-as-a-judge-confidence-escalation.md) describes a paper whose gate **q is maximum label probability**, after its two-order averaging. It is **not the service's native confidence**. At that paper's collection time the authors said the native formula was unpublished; the current docs now supply it. Keep the historical result and today's API semantics separate.
- Our [Husain/Saha eval note](decision-model-evals-thresholds-calibration.md) uses **failure probability**, which has a different meaning again: a high score can confidently indicate a bad trace. Log the field's meaning beside every threshold.
- The docs' .7/.3 Noul bands, article's .6 fraud threshold and .8/.9 confidence examples are **starting examples**. Select actual operating points from labeled deployment cases and error costs. A reported .9 probability acquires a risk interpretation through local calibration; it does not itself guarantee a 10% error ceiling under distribution shift.

## State, batching and versioning

- Send structured, relevant state with source material and current facts needed to answer the questions. Use explicit paths such as `ticket.message` to avoid indirection. Retrieve/filter before the model call; arithmetic, date ordering and exact counts belong in code.
- Ask independent questions about the same state together. Each sees the shared state, with no hidden dependency on another answer. Code decides which speculative results matter for the selected branch. Dependent questions require a later request or prior code preparation.
- TypeSafe says state is ingested once and questions run in parallel. Added questions can save round trips, but still consume tokens/context and need end-to-end latency/cost measurements. Treat the docs' roughly 100 ms and calibration claims as vendor descriptions until measured on the intended workload.
- As checked **2026-11-07**, `jev-latest` and `jev-preview` both point to **`jev-1.14.0`**. Pin a version for an evaluated policy and log the resolved response model. The existing paper tested **1.13.0**; its operating point does not automatically transfer to 1.14.
- Default documented context limits: **64k per request** (state + all questions), **32k per question** (state + that question). Larger opt-in context is available; the vendor warns of worse speed/accuracy. Keep context minimal before raising limits.

## A practical integration sequence

1. **Select one bounded workflow** and draw its decision table. Name authoritative facts, semantic questions, rule precedence, review outcomes and side effects separately.
2. **Implement exact policy in ordinary code.** Include authorization, consent, arithmetic, deadlines, idempotency and default handling. Jev supplies observations to that policy.
3. **Define atomic questions and labeled cases.** Include ambiguous requests, no-match inputs, multiple simultaneous intents, negation, conflicting context and adversarial text. Evaluate each judgment and the resulting route.
4. **Batch suitable questions and preserve raw distributions.** Record model version, question/rubric version, relevant state provenance, code facts, thresholds, selected rule and any review decision. Trace the rules as code actually executes them; do not ask Jev to invent a rationale afterward.
5. **Choose operating points on development labels and freeze them for held-out testing.** Measure precision/recall, calibration, review/escalation rate, end-to-end action errors and cost/latency. Marginally good atomic judges can compose badly when errors correlate or policy precedence is wrong.
6. **Deploy first in shadow/recommendation mode**, compare proposed routing against real outcomes, and retest after question/state/model/policy changes. Route missing, malformed or unresolved inputs through explicit failure/review paths.

**Integration sketch for our evals:** split “does this trace contain any failure?” into grounded checks such as unsupported completion, contradiction with a tool result, unresolved request and missing required evidence. Code knows whether a required tool was actually called; Jev can judge whether the claimed outcome matches the supplied evidence. Evaluate semantic checks against local labels, then combine them into a trace disposition. This is a proposed next application, not an existing deployment.

**Candidate business use:** classify a support message's refund intent with Jev; query eligibility and amount from records; let code prepare the correct approval workflow. Semantic intent is one input to the process, while authenticated authority and explicit approval govern execution.

## Known limits to design around

- Official [model-jaggedness guidance](https://docs.typesafe.ai/model-jaggedness) lists literal readings, negation/indirection, arithmetic/counting/date-comparison errors, irrelevant-state distraction, option-order effects and contradictory criteria. Test those boundaries rather than relying on the typed interface.
- The vendor explicitly says adversarial content in state can move answers. Give untrusted input a narrow interpretive role, keep secrets/authority out of model-controlled action selection, and test injection attempts. A semantic guard alone is not the authorization boundary.
- This post and docs offer architecture and examples. Existing local evaluation notes supply the separate evidence about task accuracy, threshold selection and calibration. Batched-question isolation is a useful service contract, not a guarantee that any application decision is correct.

**Why it matters here:** Jev fits as a small semantic component inside a workflow we can inspect, test and control. It can support eval checks, relevance filters and intent interpretation while deterministic code remains the source of policy and action authority.

**Sources:** [full article](https://typesafe.ai/blog/dont-call-it-a-decision-model), [building guide](https://docs.typesafe.ai/concepts/how-to-build-with-system-one), [confidence](https://docs.typesafe.ai/confidence), [companion Noul](https://docs.typesafe.ai/patterns/companion-noul), [fan-out](https://docs.typesafe.ai/patterns/fan-out), [probability routing](https://docs.typesafe.ai/patterns/probability-routing), [confidence routing](https://docs.typesafe.ai/patterns/confidence-routing), [state](https://docs.typesafe.ai/concepts/state), [models](https://docs.typesafe.ai/models), [limitations](https://docs.typesafe.ai/model-jaggedness). Retrieved 2026-11-07. [Archived article HTML](../../transcripts/evaluation/2026-11-07-typesafe-judgments-code-decisions.html), [text](../../transcripts/evaluation/2026-11-07-typesafe-judgments-code-decisions.txt), [documentation snapshot with per-page read depth](../../transcripts/evaluation/2026-11-07-typesafe-system-one-docs.json). Documentation examples were read; no live API/SDK integration tested.
