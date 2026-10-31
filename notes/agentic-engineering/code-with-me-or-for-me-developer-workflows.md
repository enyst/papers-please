---
title: "Code with Me or for Me? How Increasing AI Automation Transforms Developer Workflows"
authors:
  - Valerie Chen
  - Ameet Talwalkar
  - Robert Brennan
  - Graham Neubig
published: "2025-07-10"
updated: "2025-09-13"
source: arXiv
arxiv_id: "2507.08149"
arxiv_url: "https://arxiv.org/abs/2507.08149"
source_pdf: "https://arxiv.org/pdf/2507.08149v2"
read_depth: full
scope_note: "Full 30-page v2 PDF text, references, and Appendices A–D. Linked studies and analysis scripts not independently reproduced."
mechanism: "Compare familiar copilot workflows with novice use of an autonomous coding agent, measuring task correctness, active human effort and self-reported experience."
tags: [human-agent-interaction, cognitive-load, developer-experience, code-understanding, automation, openhands, copilot]
---

**One-line take:** In this small, short-session comparison, agents reduced reported cognitive load and increased task completion, but neither satisfaction nor understanding improved reliably; the study did not test learning or skill loss.

## Design and what was measured

- **20 participants**, recruited through university mailing lists. All used Copilot at least weekly; none reported prior coding-agent experience. Most had 3–5 years of professional programming experience. This is a largely student-recruited sample of programmers, not a representative industry survey.
- **Within-participant comparison:** randomized order of GitHub Copilot and OpenHands, 40 minutes per condition. Participants received different problems of the same task type. Task type was assigned between participants: web research/data analysis, bug fixing or feature addition. There were two problems per type, drawn/adapted from GAIA and SWE-bench.
- Conducted **April–May 2025**. OpenHands versions 0.35–0.38 used Claude Sonnet 3.7. Participants could choose the Copilot chat model; available options included GPT-4o, Sonnet 3.7, Gemini 2.5 Pro and o3-mini. Tool autonomy, interface, hosting and model choice were not independently isolated.
- Evidence: Copilot screen recordings, OpenHands event streams, final code snapshots, six comparative 5-point Likert experience items and qualitative feedback. Cognitive load and output understanding were **self-reported**, not physiological measures or independent comprehension tests. The study had no unassisted/no-AI condition.

## Results: keep the units and denominators

- **Task correctness: 25% with Copilot versus 60% with OpenHands**, p = .02. The paper calls this a “35% increase”; these means differ by **35 percentage points**, not 35% relative. Six challenging tasks and 20 participants limit generalization.
- **Human effort among correct solutions only:** 25.1 minutes with Copilot versus 12.5 minutes with the agent, p = .01. These are different time measures: the full Copilot session versus intervals around human messages for the agent, excluding autonomous action time. Agent elapsed time including its own actions averaged 27.9 minutes. This is not evidence of halving wall-clock completion time, and the correctness-conditioned comparison is not an all-participant average treatment effect.
- **Cognitive load:** 75% agreed they experienced less load with OpenHands, 10% disagreed; p = .0006. **Ability to accomplish new tasks:** 70% agreed and 5% disagreed; p = .0013. Tests compare paired-comparison Likert ratings with the neutral midpoint, rather than a standardized cognitive-load battery. The narrative swaps C1/C2 labels relative to Table 2; the percentages above follow the table and the p-values follow the named constructs in the text.
- **Speed, flow and satisfaction were mixed:** respectively p = .09, .39 and .26. Only 45% agreed they were more satisfied with OpenHands, while 40% disagreed. More completed tasks did not reliably produce a better reported experience.
- **Understanding favored Copilot descriptively:** 55% reported better understanding of Copilot outputs, versus 25% favoring the agent. p = .07, so this does **not** meet the paper's .05 significance threshold. Users described agent changes as hidden or hard to control; some said manually running and correcting bad Copilot code helped them understand it.
- **Future preference:** 60% disagreed they would continue using OpenHands over Copilot; 20% agreed (p = .04). Familiarity and novice-agent use matter here. Greater perceived competence did not imply preference for adoption.

## Where the work moved

- In both conditions, users commonly pasted the task into chat to generate the initial implementation; this was not simply autocomplete versus agent.
- OpenHands handled environment setup, package installation, file creation and debugging that Copilot users had to execute or coordinate themselves. Human work shifted toward directing, inspecting and correcting the agent.
- Participants asked where changes were made and whether the agent had deleted code. Some wanted less unsolicited work: one reported not expecting ten files with over a thousand lines each. Others described waiting without anything useful to do.
- The authors propose **transparent agent actions, calibrated proactivity and better use of human effort**. Their suggestion to support parallel tasks is a design direction, not an experimentally demonstrated multitasking benefit. They explicitly note the cognitive costs of multitasking.
- The proposed increase in verification burden with agents is a **hypothesis**; the study cannot precisely separate verification time from prompt construction or other human effort.

## What this says about cognitive load and skills

- It directly addresses **perceived effort and developer experience under greater automation**. It offers qualitative evidence of reduced contact with debugging and a possible understanding cost.
- It does **not** measure skill acquisition, pre-existing skill deterioration, delayed recall, transfer, psychological ownership or pride. Lower mental load may remove tedious setup or remove valuable learning effort; these measurements cannot distinguish those mechanisms.
- Appendix D suggests order-related differences in effort, possibly because seeing an agent attempt first teaches users an approach. The authors describe this as a possible explanation, not a demonstrated learning effect.
- Other limits: short, fixed tasks; unfamiliar repositories; uncontrolled Copilot model choice; asymmetric interfaces/time accounting; no adaptation period for agents; and no long-term maintenance. Some authors are affiliated with All Hands AI, which develops OpenHands.

## Why it matters here

- Evaluate an agent's effect on the **human**, alongside its task score. Track active review effort, independent understanding, flow and perceived control separately from output correctness and elapsed time.
- When designing explanations, include changed files, reasons, validation evidence and clear stopping points. Treat improved learning or skill preservation as hypotheses requiring an unassisted assessment.
- The [cognition, skills and ownership shortlist](ai-coding-cognition-skills-ownership-shortlist.md) identifies more direct studies of learning and delayed recall.
- [PULSE](../misc/pulse-assessing-human-agent-interactions-software-agent-design.md) studies satisfaction measurement in deployed agent sessions. Its larger scale does not turn satisfaction into a measure of skill retention.
- [Andrew Ng's skills map](ai-engineering-skills-map-andrew-ng.md) argues human fundamentals remain necessary for steering trade-offs. This controlled study supplies a human-experience measurement example, not proof of that broader thesis.

**Source:** [arXiv v2](https://arxiv.org/abs/2507.08149v2), [archived PDF](../../pdfs/2507.08149v2-code-with-me-or-for-me.pdf) and [extracted text](../../pdfs/2507.08149v2-code-with-me-or-for-me.txt). [Authors' analysis repository](https://github.com/valeriechen/copilot-agent-comparison) linked, not reproduced.
