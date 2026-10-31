---
title: "How AI Impacts Skill Formation"
authors:
  - Judy Hanwen Shen
  - Alex Tamkin
published: "2026-01-28"
source: arXiv
arxiv_id: "2601.20245"
arxiv_url: "https://arxiv.org/abs/2601.20245v2"
source_pdf: "https://arxiv.org/pdf/2601.20245v2"
read_depth: full
scope_note: "Full 31-page v2 PDF text, references and Appendices A\u2013D; image-only quiz examples and instructions checked with OCR. No reanalysis of participant data."
mechanism: "Randomize chat-based AI assistance while experienced Python programmers learn an unfamiliar library, then assess unaided conceptual understanding, code reading and debugging."
tags: [skill-formation, learning, cognitive-offloading, debugging, human-ai-interaction]
---

**One-line take:** AI access reduced immediate mastery of a new Python library in a small randomized experiment; how participants used AI correlated with learning, but the study neither randomized those usage styles nor measured long-term skill decay.

## Design: acquisition, not loss of established skill

- **52 analyzed participants, 26 per condition.** All reported more than a year of Python experience, weekly Python use, some prior AI-assistant use and no previous Trio use. Most were professional/freelance programmers; 29 had 7+ years of general coding experience. “Novice” means novice to **Trio**, not necessarily junior developer.
- Randomized between-subjects study: unaided Python warm-up, two Trio tasks with a **35-minute total limit**, then an **immediate unassisted quiz**. Treatment had a GPT-4o chat assistant that could see the current code and generate complete correct solutions. Control had documentation and web search. Neither group could use AI on the quiz.
- Tasks covered concurrent timers and record retrieval/error handling. The assessment comprised **14 questions / 27 points**, covering concepts, code reading and debugging across seven Trio topics. No independent code-writing task or delayed retention/transfer test was used.
- Both groups were told to finish quickly and warned that a quiz would follow. The treatment instructions explicitly encouraged AI use; the control stressed relying on one's own skills and avoiding detectable AI use. The intervention therefore includes instructions and access, not merely passive availability of a tool. Flat compensation was $150; learning the library was not an actual job requirement.
- Four pilots altered recruitment, task count, quiz layout and syntax hints. Early platforms had 25–35% noncompliance; the later platform enabled screen-recording checks. Pilot D found a speed benefit but also unrelated Python-syntax delays; hints were added before the main experiment. Do not combine the pilot speed result with the main trial's learning result as if from the same protocol.

## Quantitative evidence

- **Quiz:** treatment scored **4.15 raw points lower**, **Cohen's d = .738, p = .010**. Adjustment for warm-up time retained the difference (**d = .725, p = .016**). The paper describes the raw gap as “17%”; 4.15/27 is approximately **15.4 percentage points**. The stated raw denominator and percentage do not exactly agree.
- **Completion time:** no statistically significant overall difference (**p = .391**). This is inconclusive about a speed effect, not proof of equal speed. Four control participants did not finish the second task; all treatment participants did. A 35-minute cap limits interpretation of time for unfinished work.
- Exploratory quiz decomposition found the largest gap in debugging and the smallest in code reading. The subarea analysis was not preregistered; do not present every subskill as an independently confirmed treatment effect.
- Median observed errors were **1 with AI versus 3 without**. Control participants encountered more coroutine/await-related errors. Error exposure and independent resolution are plausible learning mechanisms, but were not randomized or established through causal mediation.

## Usage patterns: useful hypotheses, small observational groups

| Pattern | n | Mean quiz | Mean task time |
|---|---:|---:|---:|
| AI delegation | 4 | 39% | 19.5 min |
| Progressive reliance | 4 | 35% | 22 min |
| Repeated AI debugging/verification | 4 | 24% | 31 min |
| Generate then ask comprehension questions | 2 | 86% | 24 min |
| Generate with explanations | 3 | 68% | 24 min |
| Conceptual questions, independent implementation | 7 | 65% | 22 min |

- These personas were constructed after observing behavior. Their counts sum to **24**, while the paper discusses **25** recorded AI participants; coverage is not fully reconciled. One treatment recording was unavailable. Appendix B also says 51 recordings but parenthetically lists 25+25. These reporting inconsistencies do not change the 52-person quantitative sample, but limit exact qualitative accounting.
- Difficulty, prior ability, motivation or prompting fluency can affect both behavior and score. Asking for explanations is a **promising design hypothesis**, not a demonstrated causal remedy based on n=2–7 groups.
- Manually retyping generated code showed no notable quiz advantage over pasting it. More typing time is not a reliable proxy for engagement. Within each condition, more active coding time correlated with *lower* quiz scores, plausibly reflecting existing expertise; across conditions, the unaided group coded more and learned more. Do not flatten those different comparisons into “more keystrokes cause learning.”
- More debugging queries correlated with slower completion (**r=.43, p=.033**) and lower quiz scores (**r=−.41, p=.043**). These exploratory correlations cannot tell whether reliance caused poor understanding or difficulty led to reliance.

## Limits and why it matters here

- The authors' claim that autonomous agents would cause at least as much learning loss is **extrapolation**. No agentic workflow, autocomplete-only workflow, human tutor or alternative learning mode was tested.
- Time pressure, short library tutorials, crowd recruitment and an immediate knowledge quiz limit transfer to sustained workplace apprenticeship. A quiz gap is not evidence that previously mastered programming skills disappeared.
- For agent design, separate **producing a working answer** from **forming the user's ability to check it later**. Explanations, prediction questions and independent debugging practice are candidates to test; this paper does not validate a particular product's learning mode.
- Compare with the [48-hour recall and ownership experiment](programming-students-chatgpt-recall-ownership.md), [professional longitudinal study](ai-coding-assistants-longitudinal-developer-experience.md) and [cross-paper synthesis](ai-coding-cognition-skills-ownership-shortlist.md).

**Source:** [primary paper 2601.20245v2](https://arxiv.org/abs/2601.20245v2), [archived PDF](../../pdfs/2601.20245v2-skill-formation.pdf) and [extracted text](../../pdfs/2601.20245v2-skill-formation.txt). Full paper read on 2026-10-31; linked literature and data/code not independently reproduced.
