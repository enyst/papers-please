---
title: "Rapid alternation of conscious and suppressed stimulus representations in the primate brain"
authors:
  - Janis K. Hesse
  - Frank F. Lanfranchi
  - Conor McGrory
  - Yuelin Shi
  - Tatiana A. Engel
  - Doris Y. Tsao
published: "2026-10-16"
source: "bioRxiv preprint, v1"
doi: "10.64898/2026.10.15.759299"
url: "https://www.biorxiv.org/content/10.64898/2026.10.15.759299v1"
source_pdf: "https://www.biorxiv.org/content/10.64898/2026.10.15.759299v1.full.pdf"
read_depth: full
mechanism: "Resolve Neuropixels population activity during binocular flash suppression into rapidly alternating representations of dominant and suppressed faces, and validate the inferred states through held-out neurons, reconstructions, tuning and alternative-model controls."
tags:
  - consciousness
  - conscious-access
  - temporal-multiplexing
  - binocular-rivalry
  - face-patches
  - neuropixels
  - population-dynamics
  - temporal-selection
---

**One-line take:** The same cortical neurons alternate between rich representations of seen and suppressed images on a ~60 ms timescale while the percept remains stable; conscious access therefore needs an account of temporal selection within a population, beyond identifying a brain region or decodable content.

## The experiment and finding

- **Binocular flash suppression separates input from percept.** One image appears in one eye; a second image then flashes into the other eye. Both remain physically present, but observers predominantly see the newly flashed image. Fourteen human participants verified suppression; analysis focuses on 300–1000 ms after the flash.
- **Recordings come from two male rhesus macaques**, maintaining fixation without perceptual reports. Neuropixels probes target IT face patches ML/AM and prefrontal regions PO/PVL. The dominant/suppressed labels rely on the human-validated paradigm, not a report of the monkey's percept on each trial.
- One stimulus set uses ten screened identities across ten sessions. A separate set presents **1,500 faces** in 750 pairs across nine sessions; 60 high-repeat faces support detailed reconstructions. Priming responses to unambiguous single faces supply templates and the face-feature code.
- **Averaging hides a strong signal.** Time-averaged binocular modulation is weak, reproducing the longstanding puzzle. Splitting activity by momentary state reveals responses resembling unambiguous presentation of the dominant face in one state and the suppressed face in the other. The authors describe roughly fifteen representational switches per second; this is not fifteen perceived image switches or evidence for a universal consciousness oscillator.
- In IT, **the same neurons encode both faces in alternating epochs**, rather than separate conscious/unconscious neuron populations. A 50-feature shape/appearance model reconstructs detailed faces from state-conditioned activity. In the initial full-population analysis, some features exceed 80% explained variance; this headline analysis has circularity bias, addressed below.
- **Temporal scale:** a two-state HMM with priming-derived fixed emission templates fits only transition probabilities. Varying bin size and testing held-out-neuron likelihood gives median dwell times **64 ms and 59 ms** at the peak-likelihood 5 ms bin. This is a switching-timescale estimate, not a demonstrated periodic rhythm. Methods distinguish the autocorrelation-derived mean-dwell estimate from the HMM's median dwell.
- **The states differ beyond represented identity.** Conscious-epoch feature-tuning gain is about **1.21×** suppressed-epoch gain, with strong across-cell correspondence (`r = 0.90`). Mean firing rate is slightly higher in the suppressed state, so “more spikes = conscious” is inadequate.
- The reported **66% state-decoding accuracy** uses a paired-response ordering task: concatenate the same stimulus's state-1 and state-2 response vectors, discriminate their order, and hold out stimulus pairs. It is not a 66%-accurate online readout of subjective awareness from an arbitrary single time bin.
- **Prefrontal cortex also multiplexes**, with weaker face reconstructions but separation surviving held-out-neuron validation. Cross-patch ML↔AM coordination is weak. The data do not establish one globally synchronized cortical switch.

## Why the controls matter

- **Circular conditioning can manufacture beautiful reconstructions.** Using the same spikes to assign states and reconstruct each state sorts noise toward the chosen templates. The authors explicitly demonstrate that even static averaging and independently switching neurons can pass this initial reconstruction test. Figure 2 alone would not establish coordinated alternation.
- **The decisive test holds out neurons.** Infer states with one random half, reconstruct faces and measure tuning in the other. Representational separation survives in real IT and PFC data, and in both individual monkeys. Leave-one-neuron-out validation adds little over split-half; restricting to high-confidence epochs improves reconstruction further.
- **Within-trial balance:** equalize each trial's contributions to both states. Separation survives, arguing against a mere mixture of differently perceived trials.
- **Template shuffling:** replacing the actual pair with unrelated templates fails to reconstruct those arbitrary faces. Correct stimulus templates matter.
- **On/Off gain controls:** a four-template decoder separates excitability from represented image. Conscious/suppressed occupancy stays near 50/50 in both gain regimes, and the resulting content partition agrees ~80% with the original partition. Overall population gain cannot account for the main result.
- **Four simulated alternatives** use matched priming templates/trial structure: coordinated switching, conscious-only, static averaging, and independent switching per neuron. Only coordinated switching reproduces the full battery: reconstruction, cross-neuron reconstruction, held-out tuning reversal and held-out likelihood advantage over a one-state model. This comparison rules out these alternatives; it does not uniquely identify every possible biological dynamical model.
- **The old weak-modulation result gets a mechanistic explanation:** averaging cancels opposing state-specific selectivity, leaving a small conscious bias from stronger tuning gain. Equalizing gain removes that residual correlation in IT.

## Interpretation and the next experiment

- **Representational richness is insufficient for access.** A suppressed face can occupy the same detailed feature code in the same high-level neurons as a consciously seen face. A region, neuron or content decoder alone cannot say which representation reaches awareness.
- **The constructive hypothesis is selective routing in time.** The authors suggest that a state signature could determine which epochs reach downstream report, introspection and behavioral-control circuits. Recurrent visual interactions or feedback from parietal cortex/pulvinar are candidate routes. These are proposals; the routing mechanism was not measured or causally manipulated.
- The important follow-up is to identify the receiving circuits and perturb access conditional on an inferred epoch, while checking perception. Weak cross-patch coordination makes it especially important to test how locally multiplexed populations could support a unified percept.
- **This advances a tractable consciousness question.** It shows where anatomical averages can miss the relevant organization. The paper explicitly sets aside the hard problem. Its evidence concerns visual access under this paradigm; it neither supplies a complete recipe for generating awareness nor settles Global Workspace versus IIT or recurrent-processing theories.
- **Evidence limits worth preserving:** two animals, face-centered tasks, no simultaneous macaque percept reports, model-based state inference and no causal intervention. Data are promised through DANDI and code through GitHub upon publication; the preprint does not yet provide them for independent reanalysis. These boundaries matter to the next tests, not as a reason to dismiss the discovery.

## Connections to the corpus

- [Block: access versus phenomenal consciousness](block-two-concepts-of-consciousness.md): useful vocabulary for separating availability to report/control from experience itself.
- [Northoff: the brain's inner time](what-physics-offers-ai-brain-inner-time.md): concrete evidence that temporal population organization matters; it does not establish Northoff's broader claim that machines cannot participate in time.
- [Gurnee et al.: Jacobian Lens / workspace](../interpretability/gurnee-jacobian-lens-global-workspace.md) and [Chalmers' critique](../interpretability/chalmers-j-space-global-workspace.md): reading content and demonstrating its selective downstream availability are different experiments. Tsao's biological result motivates testing access/routing rather than equating decodability with awareness. It does not validate or invalidate J-space in transformers.
- [Cochinescu: identity as accumulated selection](cochinescu-entropy-conversational-ai-accumulated-selection.md): keep this machine-side perception-engineering proposal distinct from the biological access result. Shared selection vocabulary is a conceptual connection, not a shared demonstrated mechanism.

**Sources read:** complete **50-page [v1 PDF](../../pdfs/2026-10-16-hesse-tsao-conscious-suppressed-v1.pdf)** text, including Methods, six main and ten Extended Data figure legends, and references; [extracted text](../../pdfs/2026-10-16-hesse-tsao-conscious-suppressed-v1.txt). Figures were not independently digitized or data reanalyzed. [Primary source](https://www.biorxiv.org/content/10.64898/2026.10.15.759299v1), retrieved 2026-10-18. The `.full` HTML endpoint returned only abstract-page content, so the full reading used the PDF. [Tsao's opening announcement](https://x.com/doristsao/status/2111316522098733078), dated 2026-10-17, was read through a text mirror and [archived](../../transcripts/world-models-agi/2026-10-17-doris-tsao-announcement.json); later thread posts were not retrieved. Scientific claims above come from the paper, not an inferred thread summary.
