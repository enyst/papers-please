---
title: "Beyond Productivity: Measuring Developers' Cognitive Load During GenAI-Supported Software Development"
authors:
  - Charlotte Brandebusemeyer
  - Daniela Gasser
  - Tobias Schimmer
  - Bert Arnrich
published: "2026-09-29"
source: arXiv
arxiv_id: "2609.37645"
arxiv_url: "https://arxiv.org/abs/2609.37645v1"
source_pdf: "https://arxiv.org/pdf/2609.37645v1"
read_depth: full
scope_note: "Full 12-page v1 PDF text and references, plus full separate 3-page physiological-preprocessing supplement (Zenodo 22692764). No raw-data replication."
mechanism: "Model task-level perceived workload during industrial development using AI use, task context and wristband physiology, rather than inferring mental effort from output alone."
tags: [cognitive-load, developer-experience, field-study, physiology, wearables, observational]
---

**One-line take:** In this industrial sample, AI-assisted tasks had higher reported mental load after coarse contextual adjustment; wearable physiology added little, and neither result identifies a causal effect of AI on cognition.

## Design and measurement

- **Four days in Q2 2025**, at two SAP sites in California: 22 recruited, **21 analyzed** after a protocol exclusion. Mix of developers, senior developers, a quality specialist and an architect. Participants used Java regularly, reported prior AI use, and chose their tools and tasks.
- Paper workday logs captured task start/end, **binary GenAI use**, and a **single 7-point cognitive-load rating** per task. Developers were encouraged to use GenAI for **at least one continuous hour daily**, so this was not wholly uninfluenced naturalistic usage. Controlled sessions on days one/four are explicitly outside this paper's analysis.
- **382 logged tasks**. After physiological cleaning: **263 BVP tasks from 19 participants**, **371 EDA tasks from 21**, **371 temperature tasks from 21**. These are repeated observations, not hundreds of independent developers. Tasks were categorized as development-heavy, collaboration-heavy or other; category, duration and a participant random intercept formed the contextual model.
- Wristbands measured BVP, electrodermal activity, temperature and acceleration. Acceleration filtered movement artifacts rather than entering the outcome model. Physiological metrics were participant-standardized and skewed variables transformed.

## Main result: higher task-level perceived load

- AI use was associated with **+.996 points on the 1–7 load scale**, **LRT p<.001**, marginal **ΔR²=.047**, conditional on task category, duration and participant random intercept.
- Duration was associated with **+.007 points/minute**, **p<.001, ΔR²=.038**. Task category added the most explanatory value (**ΔR²=.091**): development-heavy exceeded collaboration-heavy by **.591 points** and other tasks by **1.437** (Tukey p=.0153 and <.0001).
- Contextual model **marginal R²=.324**, conditional **R²=.459** including participant differences. These describe fit within this dataset, not validated prediction or causal attribution.
- Important contrast: participants in the broader study generally *said* AI reduced effort, while specific logged AI tasks were rated more demanding. Global retrospective judgments and task-local ratings answer different questions; task selection can contribute to the discrepancy.

## Physiology: small, conditional signals

- Of **11 individual metrics**, only lower **skin-temperature standard deviation** significantly improved fit after Benjamini–Hochberg correction: estimate **−.224 load points per within-person SD**, **pBH=.041, ΔR²=.014**. HR/HRV and EDA added no detected independent contribution.
- The four-predictor multimodal model added **ΔR²=.019**, but its main linear-model block test was **p=.052**, **not statistically significant at .05**. The paper's “almost/nearly significant” wording should not become a positive confirmatory result.
- Temperature variability drove the nested follow-ups; removing cardiovascular or EDA components did not significantly worsen fit. This provides no demonstrated cross-modality synergy.
- Ordinal models retained the temperature direction/significance and found a multimodal block effect (**p=.028**). Collapsing the seven-point response into three categories removed the single-temperature significance (**pBH=.102**). Strength of evidence depends on model/scale resolution.
- Temperature can reflect posture, environment and peripheral regulation as well as mental demand. This is an association with self-report, **not a context-independent brain-load sensor**.

## Preprocessing supplement: what was actually checked

- [Supplement, Zenodo 22692764](https://doi.org/10.5281/zenodo.22692764), [archived PDF](../../pdfs/2609.37645v1-cognitive-load-preprocessing-supplement.pdf), [text](../../pdfs/2609.37645v1-cognitive-load-preprocessing-supplement.txt).
- Six BVP pipelines varied motion thresholds, cleaning and abrupt-HR filtering. On the **89 tasks common to all pipelines**, model fits were similar (**AIC 302.73–303.12; marginal R² .316–.320**). This robustness check applies to that common subset, not proof that exclusions cannot bias the full analysis.
- Selected “Motion” pipeline used participant/day acceleration **mean+SD** threshold, removed/interpolated high-motion segments and retained the most BVP tasks (**263/382**). More aggressive HR filtering retained only 91–172 tasks and might remove genuine variation. Temperature outside **25–40°C** was excluded; gaps were interpolated.
- The choice balances data retention and signal plausibility; preprocessing was not a measurement of true cognitive load against an independent gold standard.

## Causal limits and why it matters here

- Developers may choose AI for more complex, unfamiliar or otherwise difficult tasks. Three task categories and duration do not control task complexity, familiarity, output quality, interruptions or AI interaction intensity. **AI causes a one-point workload increase** is not supported.
- Binary AI use combines autocomplete, chat, prompting and verification. A random intercept accounts for clustering but does not isolate within-person causal changes or separate all stable user differences from selection.
- Four days, one employer, modest participant count, physiological missingness/interpolation and noisy non-cognitive signals limit transfer. No skill, recall, psychological-ownership or burnout outcome was tested.
- Use task context and explicit review/steering burden when evaluating agents. Do not substitute wristband values for competence or individual employee performance; the paper itself cautions against workplace decisions based on this sensing.
- See [six-month professional survey](ai-coding-assistants-longitudinal-developer-experience.md), [student load/recall experiment](programming-students-chatgpt-recall-ownership.md) and the [synthesis](ai-coding-cognition-skills-ownership-shortlist.md).

**Source:** [primary paper 2609.37645v1](https://arxiv.org/abs/2609.37645v1), [archived PDF](../../pdfs/2609.37645v1-developer-cognitive-load.pdf) and [extracted text](../../pdfs/2609.37645v1-developer-cognitive-load.txt). Full paper read on 2026-10-31; linked literature and data/code not independently reproduced.
