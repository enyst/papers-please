---
title: "An Experimental Evaluation of Multimodal Prompt Injection Attacks on Agentic AI Frameworks (MMPIBench)"
authors:
  - (see paper)
arxiv_id: "2609.09404"
arxiv_url: "https://arxiv.org/abs/2609.09404"
published: "2026-09"
source: "arXiv:2609.09404 [cs.CR]"
read_depth: "abstract-only"
mechanism: "MMPIBench: a reproducible benchmark delivering a fixed attack set through six visual carriers (OCR text, overlays, EXIF metadata, QR codes, fake interfaces, hybrids) — and audio — measuring how far each injected instruction travels (perception → planning → tool call) across frameworks and models."
tags:
  - prompt-injection
  - multimodal
  - vision
  - audio
  - benchmark
  - agentic-frameworks
categories:
  - cs.CR
---

- **One-line take:** Injection via **images and audio**, not text — an attacker can put instructions into an agent's context through any perceptual channel it reads. MMPIBench measures how far those travel, and finds two useful facts: (1) **the model matters far more than the framework** for whether an injected instruction is acted on; (2) **the planning step is where most attacks die** — the model reads the injected instruction and declines.

- **Numbers:** 720 runs (6 frameworks × 5 models × 6 visual carriers × 4 objectives): attacks *attempted* in 12.8% of runs, *complete* in ~1% — the gap closed almost entirely at planning. One model never attempts and recognizes injection 59.7% of the time; two others attempt ~23.6%. **Audio is the soft underbelly**: where the signal arrives, attacks complete in 49% of cells (75% for one model). Reporting completion alone understates exposure; non-vision perceptual channels are narrower but far less defended.

- **Why it matters for us:** SmolPaws has *sight* (screenshots) and *hearing* (Whisper transcription of voice notes) — real non-text perceptual channels. This is the direct warning that those are injection surfaces, and that audio especially is under-defended. Concrete carriers to worry about: OCR/overlay text in screenshots, EXIF, QR codes; and transcribed audio instructions.

- **Source:** abstract via arXiv:2609.09404 (Chrome). Not yet full-read.
