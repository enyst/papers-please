---
title: "Your Programming Students' Cognition with ChatGPT: Higher Performance, Lower Retention, and Reduced Ownership"
authors:
  - Christian Bergh
  - Benjamin Tag
  - Alexandra Vassar
  - Jake Renzella
published: "2026-09-18"
source: arXiv
arxiv_id: "2609.21194"
arxiv_url: "https://arxiv.org/abs/2609.21194v1"
source_pdf: "https://arxiv.org/pdf/2609.21194v1"
read_depth: full
scope_note: "Full 17-page v1 PDF text, all tables, references and Appendix A survey instrument. No independent data or statistical-code replication."
mechanism: "Compare AI-assisted and search-assisted introductory programming, measuring artifact performance, mental effort, immediate and delayed recall, authorship and felt ownership."
tags: [psychological-ownership, retention, learning, cognitive-load, authorship, computing-education]
---

**One-line take:** Students assisted by ChatGPT produced better code but recalled less and felt less ownership; the gap was already present immediately, with no detected extra forgetting over the next 48 hours.

## Design and exclusions

- **59 first-year CS undergraduates** at one university; gender-balanced **pseudo-random assignment** to ChatGPT-4.5 (31) or conventional Google search (28). This is not an unrestricted random sample or a professional-developer study.
- Three introductory **C** problems in fixed, increasing-difficulty order, a **30-minute total budget**, identical EdStem scaffolds and automated grading. ChatGPT memory was off and accounts were separated. The AI arm could not use web search; the control had AI Overviews disabled and major AI sites blocked. This compares two resource packages, not AI added to an otherwise identical resource set.
- **55 analyzed: 29 AI, 26 control.** Excluded one AI-assigned participant who did not use AI and three who never attempted Task 3 (one AI, two control). These are **post-assignment behavior/outcome exclusions**, so the reported contrast is not a clean intention-to-treat estimate. One excluded AI participant had tried tutoring-style interaction that became circular and failed to reach Task 3.
- Recall was assessed with the **same ten open-ended questions immediately and 48 hours later**, without submitted code. Questions mixed general concepts with task-specific implementation/edge-case details; this is not a new unassisted programming task or a broad expertise test. Three condition-blind markers scored each question 0–2; inter-rater alpha was .94. All participants completed the follow-up.

## Performance, recall and mental effort

| Outcome | AI | Search control | Evidence |
|---|---:|---:|---|
| Coding score | 89% | 69% | absolute Hedges' g=1.24; Holm p<.001 |
| Immediate cued recall | 41% | 53% | g=.71 favoring control; Holm p=.011 |
| Recall after 48 hours | 39% | 52% | g=.77 favoring control; Holm p=.011 |
| Task time, descriptive | 16.4 min | 24.1 min | No confirmatory speed test; AI timing n=28 |

- **Group×time interaction p=.391:** no detected difference in forgetting across the two assessments. This does **not** prove identical forgetting rates; it establishes that the study did not detect accelerated forgetting. Lower initial encoding/learning is compatible with the result, but not uniquely identified.
- Self-reported **mental effort** rose less in the AI arm as tasks became harder (interaction **Holm p=.047**). The **difficulty** interaction was not significant (**p=.591**). Students can recognize increasing task difficulty while exerting less effort to solve it themselves.
- Confirmatory pupil and HRV trajectory interactions were not significant (**Holm p=.308 and .853**). HRV retained only 53 task observations from 24 participants; pupil analysis retained 118 from 44. These are inconclusive physiological findings, not evidence that “brain activity fell” or that physiology confirms the subjective result.
- The five-minute copy-typing baseline was cognitively active. Negative pupil deltas mean less dilation than that reference, not absence of mental work. A Task-3 pupil contrast was exploratory and cannot override the nonsignificant confirmatory interaction.

## Psychological ownership: three distinct measures

- **Authorship credit:** a seven-level choice from “you are the sole developer” to “ChatGPT/Google is the sole developer,” with acknowledgement, secondary author and equal co-author levels. AI participants were more likely to credit the tool (**OR=13.4, 95% CI 4.0–44.8**). Only 2/29 AI participants claimed sole authorship, compared with 13/26 controls.
- **Self-attributed contribution:** percentage of submitted code participants felt was theirs. Means **44.59% AI versus 80.81% control**, **g=1.05, Holm p<.001**. This is not itself a scale of pride, legal ownership or responsibility.
- **Felt psychological ownership:** four adapted **1–5 agreement items**: “This is MY code”; “I sense that this is MY code”; “I feel a very high degree of personal ownership for this code”; and the reverse-worded “It is hard for me to think about this code as MINE.” Means **2.92 AI versus 4.30 control**, **g=1.11, Holm p<.001**, scale alpha **.94**.
- The full paper therefore supports a broader result than the initial abstract-only shortlist captured: lower **felt ownership as well as lower contribution attribution**. Neither measure directly tests professional identity, pride in craft, willingness to maintain the code, legal title or moral accountability.
- Accurate credit-sharing is a plausible part of the effect: a person who delegated more may correctly feel less authorship. The study does not show that lower ownership is necessarily harmful, that it caused poor recall, or that increasing an ownership score would improve learning. The authors interpret ownership and recall as convergent engagement signals; no causal direction was isolated.

## What remains uncertain

- **Exposure time and engagement depth are inseparable here.** The control spent longer on material; the authors deliberately did not adjust for post-treatment task time. That is appropriate for a total-effect question, but cannot establish a pure cognitive-engagement mechanism independent of exposure.
- Within the analyzed AI arm, 15 students generated solutions from prompts/scaffolds and 14 mainly wrote their own code and used AI for checking/debugging. Usage style was neither controlled nor randomized; there is no adequately tested subgroup result showing which style preserves ownership.
- Fixed task order confounds increasing difficulty with position. Same-question retesting can itself support retention. A 48-hour delayed recall gap cannot establish months-long decline in programming skill or transfer to unfamiliar problems.
- Proposed explanations through cognitive-load theory and proposed mitigations—retrieval, critique-the-AI, learner contribution—are interpretations/design suggestions, not tested interventions in this experiment.
- For agent workflows, a useful next experiment would vary meaningful human decisions, understanding checks and delegated work separately. Measure felt ownership, accurate credit, independent competence and maintenance responsibility independently. This is a research direction, not a demonstrated fix.
- See [Shen/Tamkin on new-library learning](how-ai-impacts-skill-formation.md), [BNY workplace perspectives](beyond-the-commit-expertise-ownership.md) and the [synthesis](ai-coding-cognition-skills-ownership-shortlist.md).

**Source:** [primary paper 2609.21194v1](https://arxiv.org/abs/2609.21194v1), [archived PDF](../../pdfs/2609.21194v1-programming-recall-ownership.pdf) and [extracted text](../../pdfs/2609.21194v1-programming-recall-ownership.txt). Full paper read on 2026-10-31; linked literature and data/code not independently reproduced.
