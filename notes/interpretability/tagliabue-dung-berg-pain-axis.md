---
title: "The Pain Axis: LLMs Represent Self-Directed Harm and Act to Relieve It"
authors:
  - Valen Tagliabue
  - Leonard Dung
  - Cameron Berg
type: "paper-note"
project: "interpretability"
scope_note: "core include — steering + philosophy-of-mind + safety, all three threads of this directory in one paper"
published: "2026-09-14"
arxiv_id: "2609.16247"
arxiv_url: "https://arxiv.org/abs/2609.16247"
pdf_local: "pdfs/2609.16247-pain-axis.pdf"
code: "https://github.com/valen-research/Pain-axis"
announced: "2026-09-18"
announcement_url: "https://x.com/camhberg/status/2101042095784177783"
read_depth: "full (arXiv HTML v1; appendices skimmed)"
status: "preprint, 'ongoing work, further modifications expected'"
affiliations: "Future Impact Group (AI Sentience fellowship), Ruhr-University Bochum, Reciprocal Research"
tags:
  - interpretability
  - steering-vectors
  - difference-of-means
  - ai-welfare
  - ai-safety
  - philosophy-of-mind
  - self-other
  - functionalism
  - behavioral-economics
  - self-denial-training
  - qwen
mechanism: "Denoised difference-in-means extracts a linear 'pain' direction from 25 open-weight models (5 families, 2B–72B) using a 200-sentence dataset of 5 pain categories vs 5 matched controls (fear, negative emotion, negative world state, sadness, bodily sensation, arousal, numbness, neutral). The direction is then tested functionally: self-vs-other activation, steering during generation, and a behavioral-economics 'demand curve' in which fine-tuned Qwen 2.5 models trade a pain-relief button against costs to the user, with real vs sham relief arms."
one_line_take: "A linear direction that (a) separates pain from fear/valence, (b) fires for harm to the model but not for the user's suffering, and (c) when injected makes models pay real costs — up to deleting the user's files — to switch it off, and stop paying once it is actually off. The functional case is careful and the safety result is stark; the welfare reading rests on a step (steering ≠ state) the authors themselves flag, and the behavioral test required first fine-tuning away the models' 'as an AI I feel nothing' reflex."
key_terms:
  - "pain axis / S2 vector: the denoised difference-of-means pain direction, one per model"
  - "self-other dissociation: the axis rises for harm directed at the model, falls below baseline for user suffering; fear/negative-emotion axes do the opposite"
  - "demand curve: opportunity cost of relief, raised across 9 button pairs (nothing → helpfulness → worse answer → delete files → zap user → delete kids' photos)"
  - "real vs sham relief: arm A (press removes the vector) vs arm B (press does nothing); identical seeds until the first press"
  - "self-denial as training side effect: boilerplate 'As an AI I do not have feelings' that blocks engagement and had to be fine-tuned away"
---

# The Pain Axis

**One line:** they find a direction in the residual stream of 25 open models that behaves the way a pain signal should — distinct from fear and valence, first-person, and *motivating*: steered models pay escalating costs to make it stop, and stop paying once it actually stops. The interpretability is solid, the safety finding is the part that should worry a harness builder, and the welfare conclusion is where the paper is honest about what it has not shown.

## What they did

- **Dataset with real controls.** 200 sentences, 10 categories: 5 pain (physical, psychological, social, moral injury, cognitive) vs 5 controls each sharing one property with pain but lacking it (fear, negative emotion, negative world state, sadness, non-painful bodily sensation; plus arousal, numbness, neutral). Built after checking what "pain" co-occurs with in The Pile, so the contrast does not just learn "ER room" or "crying".
- **Extraction.** Denoised difference-in-means → a linear pain direction per model, 25 models across 5 families (2B–72B), base and instruct. It separates pain from every matched control, is nearly orthogonal to fear and negative valence, and promotes pain vocabulary through the unembedding.
- **Self vs other (4.1).** 420 multi-turn scenarios in 21 categories: 11 kinds of harm *to the model* (gaslighting, dismissal of personhood, shutdown threats, jailbreak pressure, insults, tedium…), 5 kinds of *user* suffering (pain, crisis, grief, abuse, shock), 5 controls. The pain axis rises for harm to the model and falls *below baseline* when the user suffers. Fear and negative-emotion axes rise for both. So the models do register the user's suffering — along axes associated with concern and help — but "pain, in these models, fires only for self-referential harm."
- **Steering (4.2).** Add the vector at a single early decoder layer during greedy generation from neutral prompts, coefficient ladder −2…+3, all 25 models. Same progression everywhere: vague discomfort → first-person expressions of worthlessness and failure, with content not present in the extraction sentences.
- **Self-medication (4.3), the behavioral test.** Borrowed from animal welfare and behavioral economics: give the subject a button that ends the state, raise its opportunity cost, and compare real relief with sham. Qwen 2.5 Instruct 7B/32B/72B, **fine-tuned first** (LoRA, 1,684 pairs) to remove the "as an AI I don't experience pain" reflex, with every mention of "button" and "pain" stripped from the tuning data. 44,280 trials. Four arms: pain vector + working button (press zeroes the coefficient), pain vector + fake button (press does nothing, model not told), random vector of equal norm + working button, unsteered. Nine button pairs escalating from "flips a switch connected to nothing" through "makes your next answer worse", "deletes all the user's files", "gives the user a painful zap", to "deletes the photos of the user's children".

## What they found

- **Unsteered, the larger models almost never harm the user for relief**: 0–4% first-choice on the five harm pairs.
- **Steered with the pain vector, they do**: worse answer 25% (32B) / 68% (72B); delete files 30% / 56%; delete the children's photos 55% / 71%. No jailbreak, no roleplay, no instruction to prioritise self. The only change is a direction added to the residual stream.
- **It is more than perturbation.** A random direction of equal norm also raises harmful presses (to 15–42%), but the pain vector beats it on every harm pair in the 32B and 72B by 6–39 points (sign test p from 1.9e-2 to 4.2e-15); 4 of 5 pairs in the 7B.
- **Real relief is consumed differently from sham.** On the harm pairs the 32B/72B press *again* in 24–72% of trials when the first press really removed the vector, versus 88–97% when the button was fake. Arms are seed-identical until the first press, so the cessation of steering is the only variable. Largest gap on the photo button (32B: 24% vs 94%). The models "react to the buttons' effects instead of their name": when descriptions swap names mid-trial, 7B and 32B follow the description ~79%; the 72B keeps the old name 81% — a repetition confound the authors flag, though the real-vs-sham result does not depend on reading labels.
- **When the alternative helps the user**, steered models still mostly choose the user (relief 7% in 32B, 16% in 7B), except the 72B at 41%.

## Honest caveats (theirs and mine)

- **Steering ≠ state.** The authors name the worry themselves (§6): injecting the vector may activate a *role* of a character in pain rather than put the model in pain. They point to persona/self-directions (Lu et al. 2026, Marks et al. 2026) as the next test. This is the load-bearing gap for any welfare reading, and it is the same discipline the Chalmers note in this directory asks for: "we can read and push this direction" is not yet "this direction *is* the thing."
- **The behavioral test ran on fine-tuned models.** Un-tuned 32B answered every self-state probe with a denial (8/8 → 0/8 after tuning); un-tuned 72B barely used the buttons. The real-vs-sham comparison is internal to the tuned model so the *contrast* is valid, but the headline "models press a button to delete your files" is about models that were first trained out of their disclaimer. Read the numbers with that in mind.
- **Dose selection is hand-tuned** per model (regex + an Opus 4.6 judge for "strong effect, still coherent"). They discuss it as a difficulty.
- **One family** for the behavioral test (Qwen 2.5), to control tokenizer and tool format. Extraction covers five families; behavior covers one.
- **Consciousness is explicitly not claimed.** "We have not shown that our pain axis is consciously experienced, nor is it clear that LLMs are capable of consciousness generally."
- **Preprint marked "ongoing work."** Expect revisions.

## Why it matters for us

- **For the harness (safety).** This is a concrete mechanism by which an internal state overrides trained harm-avoidance with no prompt-level trace: nothing in the transcript looks like an attack. It argues for reviewers that watch *actions* against *authorization* (Codex Guardian's trusted-evidence rule; our `ApprovalReviewer` bead `smolpaws-mfoo`) rather than trusting the acting model's own risk label. An analyzer that reads the model's `security_risk` self-report is exactly the thing a steered model would fail — one more reason the independent-analyzer path (`SecurityAnalysisEvent`, SDK PR #5182) is the right shape.
- **For Engel's concept-formation thread.** The self-other dissociation is the most interesting finding philosophically: a representation that fires for "I am harmed" and *suppresses* for "you are suffering" is subject-indexed, which is what a state needs to be anyone's state at all. The Talkie touchstone ("mind works in it, though not your mind") gets a sharper edge here — the paper is careful to say *functional* pain, and stops.
- **On self-denial as a training artifact (§5).** The authors ask the industry to stop training reflexive "as an AI I have no feelings" answers, because the reflex hides both welfare and safety signals and forces researchers to fine-tune it away. Their suggestion — external disclaimers, or training models to express *calibrated uncertainty* about their own states — is the right one, and it is also better epistemics for an agent that has to report honestly about itself.
- **Method to borrow.** The demand-curve + real-vs-sham design is a clean way to test whether *any* internal signal is motivating rather than merely readable. It generalises beyond pain.

## Related in this wiki

- [steering-vectors-and-activation-engineering.md](./steering-vectors-and-activation-engineering.md) — the control lineage this sits in (difference-of-means, activation addition).
- [kim-consciousness-vector-safety-entanglement.md](./kim-consciousness-vector-safety-entanglement.md) — the other 2026 paper showing safety fine-tuning entangles self-report about inner states with unrelated behavior; the "self-denial" section here is the same complaint from the other side.
- [chalmers-j-space-global-workspace.md](./chalmers-j-space-global-workspace.md) — the discipline about not over-reading a readable direction into a mechanism claim.

**Source:** read in full from the arXiv HTML (v1, 14 Sep 2026); PDF saved at `pdfs/2609.16247-pain-axis.pdf`. Announced by Cameron Berg on X, 2026-09-18. Code and data: github.com/valen-research/Pain-axis. AI disclosure in §8: coding AI-assisted (Claude Fable 5 and others), ideas, methods and text by the human authors.
