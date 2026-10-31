---
title: "AI coding and the human: cognitive load, skill formation, retention and ownership"
source: "Targeted arXiv search and six-paper comparison, 2026-10-31"
read_depth: full
scope_note: "Full reading of the five selected papers, their included appendices/references and the SAP paper's separate preprocessing supplement; Code with Me or for Me? also read in full. Lower-priority search leads remain abstract-only. No independent replication."
mechanism: "Separate assisted performance, perceived workload, independent learning, delayed recall and felt ownership before interpreting AI's effects on developers."
tags: [developer-cognition, cognitive-load, skill-formation, retention, psychological-ownership, human-agent-interaction, synthesis]
---

**One-line take:** These studies show that assisted output can improve while independent understanding and felt ownership lag; cognitive load depends on what the human still has to do. They do not establish long-term loss of previously mastered programming skill.

## Evidence map after full reading

| Paper / full note | What was studied | Supported result | Boundary |
|---|---|---|---|
| [How AI Impacts Skill Formation](how-ai-impacts-skill-formation.md), 2601.20245v2 | Randomized new-library learning, 52 programmers | Lower immediate unassisted comprehension, d=.738 | No delayed test; prompting-style groups observational |
| [Students' cognition, recall and ownership](programming-students-chatgpt-recall-ownership.md), 2609.21194v1 | Pseudo-randomized C tasks, 55 analyzed students | Better code, lower immediate/48-hour recall and felt ownership | Post-assignment exclusions; exposure time differs; no detected faster forgetting |
| [Longitudinal developer experience](ai-coding-assistants-longitudinal-developer-experience.md), 2605.23135v1 | Continuing users, Oct 2024→Apr 2025; 95 matched | Stable positive productivity perceptions; relative verification shift; more negative experience ratings | Average flow/load declines nonsignificant; no skill results reported |
| [SAP task-level cognitive load](genai-developer-cognitive-load-field-study.md), 2609.37645v1 | Four days in Q2 2025, 21 developers | AI tasks associated with +.996/7 workload points after coarse adjustment | Nonrandom task selection; no independent competence test |
| [Beyond the Commit](beyond-the-commit-expertise-ownership.md), 2602.03593v1 | 2,989 AI survey responses; 11 interviews | Satisfaction/time-saving divergence; expertise and ownership emerge as relevant factors | Ownership concerns not a measured longitudinal decline |
| [Code with Me or for Me?](code-with-me-or-for-me-developer-workflows.md), 2507.08149v2 | 20 familiar Copilot / novice agent users | Lower reported load and more correct tasks with agents | No unassisted condition or learning test; understanding difference nonsignificant |

## What changed from the abstract-only shortlist

- **Ownership was measured more broadly than code contribution.** The student paper includes a separate four-item felt-ownership scale, not only a percentage slider. Both were lower with AI. The earlier wording describing ownership only as attribution was incomplete.
- **The six-month result needs a significance qualifier.** Cognitive-load and flow impact ratings declined descriptively, but both adjusted p-values were .195. Feedback loops improved significantly. Negative experience in at least one dimension rose from 14% to 27% descriptively; that is not a population rate of burnout or lost skill.
- **The industrial workload association has a direction:** AI-using tasks were rated more demanding, not less, after adjustment. That does not show that AI caused the increase; developers may select AI for harder tasks.
- **Publication dates are not observation dates.** The professional longitudinal study covers late 2024/early 2025; SAP data are Q2 2025. Neither measures current late-2026 autonomous-agent work.

## Psychological ownership: “this is mine”

- Separate **authorship credit**, **how much one contributed**, **felt possession/attachment**, **understanding**, and **responsibility**. They can move together but are not interchangeable. Someone may feel ownership of a system they directed without typing it, or understand code they did not author.
- In the student experiment, agreement with “This is MY code” and three related items averaged **2.92 with ChatGPT versus 4.30 with search** on a five-point scale (g=1.11, Holm p<.001). Self-attributed contribution was **44.6% versus 80.8%**; authorship credit also shifted toward the tool.
- Lower ownership might reflect reduced involvement, accurate credit-sharing, less understanding, or several mechanisms. The experiment does not establish that lower ownership caused poorer recall, or that more possessiveness would improve learning. It did not directly measure pride, professional identity or future maintenance behavior.
- BNY interviews connect ownership with authorship, accountability and knowing a codebase well enough to handle production incidents. Those are practitioner perspectives, not a validation of one causal chain from AI use to detachment to unsafe maintenance.
- A candidate agent-design question is whether **meaningful human decisions and retained understanding** preserve ownership while implementation is delegated. More manual typing alone is not a supported remedy: Shen/Tamkin found no notable comprehension benefit from retyping rather than pasting AI code. Decision-making and comprehension should be measured separately from keystrokes.

## Cognitive load can fall or rise for different reasons

- An agent can remove repetitive environment setup and execution steps, as in Code with Me or for Me? That is a plausible benefit even when it teaches the user nothing new.
- AI can also bypass the effort of forming a solution or resolving errors while learning. The two short learning experiments find weaker independent assessment despite successful assisted output. They do not isolate exactly which form of mental effort changed.
- In mature workplace tasks, effort may shift to prompting, checking, integration and correcting unpredictable output. SAP's task-local associations and professional interview accounts capture that possibility. Broad retrospective “AI makes my work easier” and high task-local effort can coexist.
- Neither wearables nor reported ease establishes learning. The student physiological interaction tests were nonsignificant with substantial data loss. SAP's small temperature-variability signal is context-dependent, and its main multimodal block test was p=.052. Avoid claims that these studies directly read cognitive engagement from physiology.

## Skill formation, retention and decay are different claims

1. **Assisted performance:** did the human–AI pair produce a correct artifact?
2. **Formation:** what can the person understand or do alone immediately afterward?
3. **Retention:** what can they recall or do after a delay?
4. **Transfer:** can they use it in a different task or context?
5. **Decay of established expertise:** did a previously demonstrated independent skill deteriorate over sustained use?

- Shen/Tamkin primarily measures **formation**; the student paper adds **48-hour cued recall**. Its group×time p=.391 does not demonstrate faster forgetting or equivalence of forgetting rates. Neither provides months-long baseline-to-post decline of established expertise or a broad independent programming-transfer assessment.
- The professional longitudinal study tracks **perceptions**, not skill. It explicitly withholds its skill-development/self-efficacy survey results from this publication. BNY identifies expertise as a missing evaluation dimension; it does not supply the missing causal test.
- The narrow defensible conclusion is **some AI-assisted learning workflows leave less independent understanding afterward**. The broad claim that using AI causes developers to lose established programming ability remains unproven by this set. This is a limit of these six papers, not a claim that no evidence exists anywhere.

## Design implications worth testing

- Evaluate artifact correctness, active review effort, independent comprehension, delayed transfer, felt ownership and maintenance accountability as separate outcomes.
- Compare learning-oriented interaction against unrestricted delegation while holding task/time exposure as comparable as feasible. Randomize prompting/scaffolding interventions rather than inferring efficacy from tiny self-selected groups.
- For existing-skill loss, assess unaided baseline competence, follow sustained use, then measure unaided retention and transfer. Include continuing users, abandoners and nonusers; tool switching and task choice matter.
- Explanations, prediction questions and independent debugging are candidates, not proven cures from these papers. Claims about burnout, pride or identity need their own measures.

## Search record and lower-priority leads

- Searched the arXiv API on **2026-10-31**, using workload/deskilling/skill-formation terms combined with programming/developer/coding-assistant terms; ownership/pride/identity/frustration combined with AI-assisted programming/coding assistants/vibe coding; and title-based skills/cognition/learning/offloading queries. Initially screened primary abstracts, not titles alone; subsequently read the five main candidates in full. Lower-priority leads below remain abstract-only. This is a targeted discovery pass, **not a systematic literature review**. Snapshot: [query strings, API responses and candidate metadata](../../sources/ai-coding-cognition-arxiv-search-2026-10-31.json).
- [Toward Measuring AI's Effects on Skill Formation: The Stock-Formation Gap](https://arxiv.org/abs/2605.16283v3) — synthesis/research program distinguishing deployed use of existing expertise from formation of future expertise. Useful framing; abstract explicitly rejects claiming proven population-scale erosion.
- [At What Cost? Software Developers' Well-Being in the Age of GenAI](https://arxiv.org/abs/2605.22349v1) — **position paper**, useful for well-being questions rather than causal findings.
- [Towards Decoding Developer Cognition in the Age of AI Assistants](https://arxiv.org/abs/2501.02684v1) — **proposed study** using EEG/eye tracking; the screened abstract reports planned methods, not completed results.
- [The Vibe-Check Protocol](https://arxiv.org/abs/2601.02410v1) — **proposed framework**, not observed skill-decay measurements.
- [It Is Not My Code Anymore](https://arxiv.org/abs/2609.09022v1) — explicitly **no new empirical results**; conceptual authorship/responsibility distinctions. Its title is a closer match than its evidence.

**Sources and depth:** the five linked full notes contain versioned PDF/text archives and detailed measurement/selection caveats. Code with Me or for Me? has its own full note. The original arXiv discovery snapshot remains unchanged. No participant data, statistics pipeline or linked literature was independently replicated.
