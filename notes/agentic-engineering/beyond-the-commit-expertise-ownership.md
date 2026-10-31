---
title: "Beyond the Commit: Developer Perspectives on Productivity with AI Coding Assistants"
authors:
  - Valerie Chen
  - Jasmyn He
  - Behnjamin Williams
  - Jason Valentino
  - Ameet Talwalkar
published: "2026-02-03"
source: arXiv
arxiv_id: "2602.03593"
arxiv_url: "https://arxiv.org/abs/2602.03593v1"
source_pdf: "https://arxiv.org/pdf/2602.03593v1"
read_depth: full
scope_note: "Full 9-page v1 PDF text, tables and references. Broader confidential survey and interview data not available or independently analyzed."
mechanism: "Combine workplace satisfaction/time-saving surveys with interviews to identify short- and long-term dimensions missing from narrow AI productivity metrics."
tags: [developer-experience, ownership, expertise, productivity-measurement, interviews, copilot]
---

**One-line take:** Developers valued expertise and ownership alongside output, but this workplace study measures perspectives and proposes evaluation factors; it does not demonstrate long-term skill decline or a causal loss of ownership.

## Evidence and denominators

- At **BNY Mellon**, a larger developer survey had roughly 8,000 respondents. The AI-specific questions received **2,989 responses** according to abstract/methods/figure caption; paired analysis used **2,754**. Section 4.1 instead says **2,898**—an internal reporting discrepancy worth retaining, not resolving by guesswork.
- Two AI questions: **Copilot satisfaction** on five ordered levels and **estimated weekly time saved** in five bins. Both are **self-report**; the paper calls estimated time an objective metric, but it was not directly observed. Acceptance/usage telemetry could not be reliably obtained across developers.
- **86% satisfied/very satisfied**, yet roughly **60% reported less than an hour saved weekly**. Paired satisfaction/time-saving **Pearson r=.34, p<.0001**. Correlating ordinal bins this way is a coarse association, not a causal or interval-scale productivity estimate.
- A separate purposive/snowball sample of **11 interviewees**, spanning early-career, mid-career and managers, completed 30–45-minute interviews. Six proposed factors came from inductive descriptive thematic analysis. The large survey did **not** administer validated scales for all six factors, especially ownership and expertise.

## Six factors and what participants meant

1. **Self-sufficiency:** less need to ask coworkers or switch between documentation/search. Independence from colleagues can coexist with dependence on AI; this is not the same as independent programming competence.
2. **Frustration/cognitive load:** repetitive wrong suggestions, prompt reformulation, and effort needed to inspect or integrate responses. Fast generation can coexist with greater interpretation effort.
3. **Task completion and quality:** throughput, useful functionality and business impact, rather than raw lines produced. Interviewees wanted actual measures beyond estimated time saved.
4. **Peer review:** reviewing inappropriate optimizations and checking untested junior output can transfer costs to teammates; AI can also summarize changes for reviewers.
5. **Technical expertise:** interviewees worried that working code can bypass learning from implementation and stack traces. Others saw AI as a way to learn unfamiliar security concepts or avoid obsolete low-level skills. These are **concerns and opportunities**, not longitudinal skill measurements.
6. **Ownership of work:** perceived authorship, accountability and intimate code knowledge, including knowing where to look during a production incident. “Nothing like doing it yourself” captures a participant preference, not a universally established psychological mechanism.

## Task context changes the assessment

- **New features:** quick starting points and lower immediate effort, alongside concerns about junior overreliance, expertise formation and ownership.
- **Improving existing/legacy code:** understanding context can dominate the small edit. More generated lines do little when the hard work is locating and interpreting the right change. Interviewees reported difficult steering and review costs.
- **Tests/documentation:** boilerplate work often benefited, but selecting the scenarios to test still required thought. The paper does not independently verify the claimed magnitude of interviewees' time savings.
- These mappings are qualitative interpretations of reported use cases, not an experimental comparison of task classes.

## Operationalization, not demonstrated long-term effects

- Proposed questions cover fatigue on AI-heavy days, prompt-reformulation time, reviewer trust, onboarding, retained expertise, authorship/accountability and willingness to maintain code. They are a **research/evaluation agenda**, not validated scales or measured rates in this paper.
- No psychological-ownership scale, independent comprehension test, long-term retention assessment or randomized assistance was administered. Agentic workflows were out of scope. One company, volunteer participation and corporate tooling constrain generalization.
- The [student experiment](programming-students-chatgpt-recall-ownership.md) supplies a direct felt-ownership measure; this paper instead explains why ownership could matter to practitioners. Do not equate accurate attribution, familiarity, incident responsibility and emotional attachment merely because interviews group them together.
- For agent evaluations, combine task output and reviewer effort with independent understanding and maintenance ability. Distinguish reported satisfaction from observed benefit. See the [synthesis](ai-coding-cognition-skills-ownership-shortlist.md), [professional longitudinal study](ai-coding-assistants-longitudinal-developer-experience.md) and [copilot/agent experiment](code-with-me-or-for-me-developer-workflows.md).

**Source:** [primary paper 2602.03593v1](https://arxiv.org/abs/2602.03593v1), [archived PDF](../../pdfs/2602.03593v1-beyond-the-commit.pdf) and [extracted text](../../pdfs/2602.03593v1-beyond-the-commit.txt). Full paper read on 2026-10-31; linked literature and data/code not independently reproduced.
