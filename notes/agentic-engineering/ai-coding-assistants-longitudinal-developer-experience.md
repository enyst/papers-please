---
title: "The Impact of AI Coding Assistants on Software Engineering: A Longitudinal Study"
authors:
  - Annie Vella
  - Kelly Blincoe
published: "2026-05-22"
source: arXiv
arxiv_id: "2605.23135"
arxiv_url: "https://arxiv.org/abs/2605.23135v1"
source_pdf: "https://arxiv.org/pdf/2605.23135v1"
read_depth: full
scope_note: "Full 28-page v1 PDF text, tables and references. Separate replication package and unreported survey constructs not analyzed."
mechanism: "Follow continuing professional AI-tool users across two questionnaires to compare perceived task allocation, productivity and developer experience."
tags: [developer-experience, longitudinal, flow, cognitive-load, supervisory-engineering, self-report]
---

**One-line take:** Continuing AI users reported sustained productivity benefits and a relative shift toward verification; more crossed into negative experience ratings, but average declines in load and flow were not statistically significant.

## What “longitudinal” means here

- Questionnaires ran in **October 2024 and April 2025**, despite the paper's May 2026 publication. This is not a six-month study of late-2026 coding agents.
- **158 eligible responses initially, 101 at follow-up, 95 matched** participants. Item-complete analyses used **88** for task focus and **94** for experience. Eligibility required being a professional engineer **currently using AI coding assistants**; people who stopped using them were absent from the eligible analysis.
- Convenience/referral recruitment through professional networks, social platforms and organizations; 85% men, 41% New Zealand at baseline. Most were mid-career or senior. No randomized AI exposure, non-user control, direct observation of time allocation or objective productivity measurement.
- The survey measured changes in six work activities and three DevEx dimensions using mostly **single Likert items**. The creation/verification groupings are theoretical, not validated subscales (low internal consistency). Reflexive thematic analysis was performed by the first author with supervisory discussion, not independently double-coded frequencies.
- The instrument also asked about **skill development and self-efficacy**, but the authors explicitly state those data are **not reported in this paper**. Do not treat the existence of those questions as evidence about skill loss.

## Results with the significance boundaries retained

- **84% perceived improved productivity at both waves**; these are wave-specific descriptive percentages among continuing users. Among 95 matched participants, 77% kept identical ratings and the paired change was not significant (**p=.326**). No participant moved to negative productivity perceptions.
- **Feedback loops improved significantly** among 94 matched participants: mean **3.73→3.95**, **Holm p=.038**, rank-biserial **r=.38**.
- **Cognitive-load impact ratings: 3.74→3.60; flow: 3.54→3.36**. Both declines were **nonsignificant after Holm correction, p=.195**. The means remained above the neutral midpoint. This corrects an overstrong reading of the abstract's “eroding” language.
- The proportion with **at least one negative DevEx dimension** rose descriptively from **14% to 27%**. That is a threshold-defined subgroup result, not a direct measure of burnout, a demonstrated average decline or the proportion who lost coding skill. Within the negative subgroup, flow complaints were most common. Only 9% stayed unchanged on all three dimensions.
- Cross-sectional productivity/experience correlations existed at both waves, but **changes in experience did not significantly correlate with changes in productivity** (smallest adjusted p=.313). This supports measuring them separately; it does not establish that AI causally decouples them.

## Where effort appeared to move

- By follow-up, **82% reported less time writing code**. None of the six individual task changes reached significance after correction. Testing and reviewing trended upward, but testing still averaged below neutral; avoid saying “everyone spent more time testing.”
- The **verification-minus-creation balance** rose **.26→.53**, **Holm p=.006, r=.39** (n=88). Creation and verification averages separately were not significant (**p=.092 and .060**). This is a relative shift on perceived-change scales, not measured hours transferred between activities.
- Qualitative accounts described fewer boilerplate/manual implementation tasks, replacing search with AI questions, easier entry into unfamiliar technologies, and repeated prompting, checking and correction. Some described less flow despite faster progress; others described better understanding and confidence.
- The proposed label **“supervisory engineering work”** covers directing, evaluating and correcting AI. The authors explicitly leave its empirical distinctness from ordinary design/review/testing for future research.
- Tool combinations changed for **82% of matched participants**; mean tools per person rose **1.9→2.9**. Changes may reflect tools, task mix, experience or adaptation rather than a stable treatment maturing over time.

## Limits and why it matters here

- **40% attrition**. Retained/lost groups did not differ significantly on six measured demographic/context variables, but that does not rule out attrition by unmeasured attitudes or experience. Continuing-user selection can overstate benefits and miss abandonment.
- Retrospective self-report, changing comparison standards, single-item measures and one researcher's interpretation limit causal and population claims. Software-development perception is meaningful evidence, but is not a stopwatch, a cognitive test or a verified throughput metric.
- For SmolPaws/agent workflows, monitor review effort, interruptions and experience alongside output. A fast response may improve feedback while repeated supervision fragments concentration. The mechanism is plausible from accounts, not experimentally isolated here.
- Compare [task-level SAP workload](genai-developer-cognitive-load-field-study.md) with [short copilot-versus-agent sessions](code-with-me-or-for-me-developer-workflows.md); their different populations and measurement levels explain why “AI reduces load” is too broad. See the [synthesis](ai-coding-cognition-skills-ownership-shortlist.md).

**Source:** [primary paper 2605.23135v1](https://arxiv.org/abs/2605.23135v1), [archived PDF](../../pdfs/2605.23135v1-coding-assistants-longitudinal.pdf) and [extracted text](../../pdfs/2605.23135v1-coding-assistants-longitudinal.txt). Full paper read on 2026-10-31; linked literature and data/code not independently reproduced.
