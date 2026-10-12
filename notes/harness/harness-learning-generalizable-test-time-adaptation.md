---
title: "Harness Learning Enables Generalizable Test-Time Adaptation"
authors:
  - Alvin Zhang
  - Xuecheng Liu
  - Zixuan Wang
  - Fahim Tajwar
  - Daman Arora
  - Ruslan Salakhutdinov
  - Daniel Khashabi
  - Yuda Song
  - Andrea Zanette
published: "2026-09-28"
source: arXiv
arxiv_id: "2609.35738"
arxiv_url: https://arxiv.org/abs/2609.35738
source_pdf: https://arxiv.org/pdf/2609.35738v1
mechanism: "Train a proposer with execution-based RL to revise a frozen solver's executable harness; reuse that revision policy with development feedback on unseen tasks while both models stay frozen."
read_depth: full
tags: [harness, meta-learning, reinforcement-learning, test-time-adaptation, executable-programs, retrieval, feedback, evaluation]
---

# Harness Learning Enables Generalizable Test-Time Adaptation

**Take:** A small model can learn a transferable harness-editing procedure and keep improving code at test time; the strongest evidence is held-out task transfer, with important limits from baseline strength, graded feedback and unmatched adaptation compute.

## What learns, what adapts

- **Two models, different jobs.** A proposer reads a task description, parent harness and execution report, then produces a code revision. The solver executes inside the revised Python program. Training updates only the proposer; inference freezes both models and changes the program (§§4–5).
- **The learned object is a revision rule.** The outer loop trains the proposer across revision contexts. The inner loop applies that proposer repeatedly to a new task. Here a task means a reasoning family or QA benchmark, with multiple feedback/scoring/evaluation questions; this is not independent scaffold generation for every user question.
- **Immediate reward, not long-horizon credit assignment.** The formal objective is final adapted-harness quality, but GRPO rewards each candidate's own score plus validity. Multistep training changes which parent programs the policy encounters; it still optimizes a greedy surrogate rather than credit across rounds (Eq. 5–6, §6.3).
- **Separate feedback, selection and evaluation.** Training report questions and reward questions are disjoint. Held-out evaluation questions do not supply adaptation feedback or choose revisions. During inference, Reasoning Gym uses the same development questions for feedback and selection; QA keeps those roles disjoint within each round. Do not collapse these three sets into “the test set.”
- **Interfaces differ by experiment.** Reasoning Gym uses structured SEARCH/REPLACE edits, a diagnosis/change manifest and validation retries. QA asks for a diagnosis plus a Python code block defining `run`, capped at 200 lines. The proposer receives externally generated reports; it does not independently inspect code or run its own diagnostic tests (Appendices D–F).

## Training recipe

- **Reasoning Gym:** Qwen3.5-4B proposer and frozen non-thinking Qwen3.5-4B solver. SFT uses 432 successful first-round Qwen3.6-35B-A3B teacher revisions from 21 families; LoRA rank 32, roughly 2.9 epochs selected through family-disjoint cross-validation. RL uses five families, 640 contexts (440 seed parents, 200 stronger parents), eight candidates/context and 40 contexts/update. Sixteen updates; headline checkpoint is update 10 (Tables 4–7).
- **Validity is a substantial shaping reward.** Parse + apply + completed-trial fraction contribute up to **0.30**, even when every answer is wrong. Task reward includes partial grader credit. No-change responses execute the parent rather than receiving an automatic zero (Eq. 8).
- **SFT screening is stronger than development improvement alone.** Accept score ≥ max(seed + 0.08, 0.40), screen answer echoing/duplicates/interface violations, then use Claude Opus 5 reviewers to inspect/re-execute on development, held-out and format-varied questions for memorization, oracle access and grader exploitation. No held-out question text enters SFT completions. **Qualification:** held-out execution participates in corpus screening; this is not a pipeline whose entire data curation uses development results only (Appendix B.2).
- **QA:** separately trained Qwen3-4B proposer, frozen non-thinking Qwen3-8B solver; direct RL without teacher SFT, trained only on HotpotQA. Each context uses six feedback questions and 64 disjoint reward questions from a 2,000-question training pool. Eight candidates, four contexts/update, 320 contexts/80 updates; reward = exact match + 0.10 validity (Tables 21–22).
- **Single-step versus multistep is domain-specific.** QA single-step parents are always the seed; multistep parents come from 32 online ten-visit revision runs, with otherwise shared settings. Reasoning Gym “single-step” already includes stronger parents; its multistep run continues from that checkpoint through two offline state-refresh phases. These are not interchangeable ablations (Appendices B.3–B.4, D.2).

## Reasoning: transfer is real, baseline dominance is not

Eight independent proposals per family; each runs on 75 held-out questions after receiving feedback from 25 development questions. Means include every proposal slot, including zero-scoring harnesses. Failed edits/no-change retain the parent score under the main protocol (Table 9).

| 21 unseen families | Mean proposal score | Oracle best-of-eight |
| --- | ---: | ---: |
| Base proposer | 0.32 | 0.63 |
| SFT | 0.49 | 0.78 |
| Single-step RL | **0.62** | 0.83 |
| 35B teacher | 0.56 | **0.85** |
| Fixed generic Python tool loop | **0.69** | — |

- **The 4B beats the teacher on average, not on oracle peak.** More reliable proposals matter even when the larger model occasionally finds a better one. Oracle best-of-eight chooses by held-out score; it measures proposal potential, not a deployable selector.
- **The hand-written tool baseline matters.** A shared five-turn Python-execution loop scores **0.69**, above learned mean **0.62**. Learning improves editing over Base/SFT and the teacher, but this headline does not establish that learning is necessary to beat a generic tool scaffold (Table 9; Appendix B.1).
- **Five difficult unseen families are excluded from the main figures.** `ab`, `knight_swap`, `letter_jumble`, `modulo_grid`, `sokoban`. Across **all 26 unseen families**, means are Base **0.282**, SFT **0.415**, RL **0.528**, teacher **0.501**. Transfer persists; the reported 0.62 is a selected-subset result, not the full unseen suite (Appendix B.1).
- **Sequential adaptation:** five rounds, one candidate/round, promote only on strictly higher development score. On the 15 shared unseen families, this approaches or exceeds oracle best-of-eight independent revision. Parent programs, reports, branch instructions and selection differ, so the comparison does not isolate the causal benefit of feedback (§5.2; Appendix B.1).
- **Sequence training gives mixed gains.** Over expanded 24-family evaluations, round-five canonical held-out means are Base **0.593**, SFT **0.698**, single-step RL **0.699**, multistep RL **0.701**. Format-varied: **0.498 / 0.688 / 0.725 / 0.649**. Family lists differ by format and extra families partly follow earlier single-step performance; these are not an unbiased common-suite comparison (Tables 12–14).
- **No reliable advantage from fixed later-round training states.** Round-five development score **0.615** versus single-step RL **0.660**; paired difference −0.045 ± 0.048 standard error over twelve families. Seeing later states alone is insufficient evidence of better iterative editing (Appendix C.3).

## QA: summaries for searching, passages for answering

- **Seed bottleneck:** retrieve twice; summarize passages to form the next query; answer from summaries. A common adopted RL edit keeps the summaries for query generation but gives the final answering call **both hops' original passages**. Other edits add a third hop or retrieve again when the draft answer does not appear in evidence (Figures 7, 12).
- **Transfer scope:** train HotpotQA, evaluate unseen MuSiQue and 2WikiMultihopQA. HotpotQA retrieves over 5.23M Wikipedia abstracts. OOD corpora are smaller pools of all support/distractor paragraphs supplied with development questions, deduplicated by title/text: 21,100 MuSiQue and 54,957 2Wiki paragraphs. This is benchmark-conditioned retrieval, not unrestricted web research (Table 21).
- **Selection differs from reasoning.** Four independent chains, ten rounds each, eight candidates/round. Select the highest development-scoring candidate **even if worse than its parent**; keep the parent only if all candidates fail. Feedback/scoring questions can recur across rounds, but remain disjoint within a round. Evaluation questions remain separate (Appendix D.3).

Independent proposal results, each row over 80 attempts (Table 23):

| Dataset | Seed EM | Single-step RL mean | Multistep RL mean | Best-of-80, single / multi |
| --- | ---: | ---: | ---: | ---: |
| HotpotQA | 0.3900 | 0.4105 | 0.4131 | 0.5800 / 0.5833 |
| MuSiQue | 0.1438 | 0.1467 | 0.1551 | 0.2408 / 0.2408 |
| 2Wiki | 0.2500 | 0.3090 | 0.2748 | 0.5200 / 0.5433 |

- **Repeated revision reveals more than the one-edit mean.** MuSiQue single-step RL rises from about **0.15** for independent proposals to **0.27** after ten rounds. On both OOD benchmarks, each trained policy's final-chain mean exceeds its oracle best-of-80 independent result. Both trained policies finish above Base on all three benchmarks; sequence training reaches roughly the same final scores as seed-only training (§§5.3–5.4).
- **Proposal count is matched per chain; compute and feedback are not.** One chain consumes 80 proposals; the four-chain mean and best-run statistics use **320** total. Independent proposals share four seed reports; chains get intermediate-program feedback. Best across all chains/rounds is not comparable at equal budget to best-of-80. Extra solver calls/retrievals and repeated development scoring also cost work (Appendix D.4).
- **The validation branch is a heuristic.** An answer appearing in a passage can trigger acceptance, but occurrence alone does not establish that the passage supports the answer. The paper reports usefulness in these QA benchmarks, not a general factuality guarantee.

## Reliability and composition: correct helper code is not enough

- **RL increases viable proposal supply.** On five unseen-family reliability probes, failed/zero-scoring rate drops Base **38%**, SFT **35%**, RL **8%** (40 attempts/method). Invalid code and valid-but-wrong code are counted separately; zero score does not imply invalidity. Dropping zero-scoring attempts can reverse teacher comparisons (Tables 10–11).
- **Most reasoning edits rediscover interpreter loops.** These comprise 48% of SFT demonstrations and dominate trained proposals without a helper directive. Helpers integrated structurally into a solver loop rarely contribute functionally: one directive audit finds SFT **11/24 structural, 4/24 functional**, RL **12/32 structural, 3/32 functional** (Table 17).
- **Prompts and rewards do not guarantee the desired architecture.** A guarded “helper with solver fallback” directive produces direct algorithmic solutions in 158/160 draws, with zero structural/functional compositions. Under a tool-use reward, composed loops fall from 25/40 at initialization to 1/40 at checkpoint 14. Combined rewards retain more composition but do not beat single-step RL in repeated revision (Tables 17, 19).
- **The failure sits at interfaces.** Correct BFS, Sudoku backtracking or a prime sieve can still fail because the parser misses a goal marker, tool messages are malformed or answer extraction returns an unsolved grid. Score helper contribution end-to-end, not just helper code correctness (Table 20).
- **Training variants bundle changes.** Harder-task RL changes data and validity rewards plus adds a composition bonus, but no rollout passes the structural screen, so the bonus never contributes. Its 19-family evaluation mixes seen/unseen tasks. These probes do not cleanly identify which reward term caused a gain (Appendix C.3–C.4).

## Limits and why it matters for us

- **Requires graded development feedback.** Reports include expected answers, answer correctness and, for QA, retrieved/missed gold supporting documents. This demonstrates adaptation when task feedback is available; it does not establish autonomous improvement on arbitrary unlabeled personal-agent work.
- **Two separately trained proposers, fixed solver within each domain.** No demonstrated reasoning→QA editor transfer, coding deployment, changing-solver robustness, indefinite continual learning or long-horizon cross-round credit assignment. The authors frame these as future work, not completed results (Appendix F).
- **Replication detail has gaps.** Appendix E gives schematic prompts rather than the complete production prompts. QA response/time budgets also differ between Table 22 and the following sampling paragraph. No project/code release URL is supplied in the PDF. Treat numerical replication as requiring implementation clarification.
- **Adds a distinct step to the harness genealogy.** [Meta-Harness](meta-harness-end-to-end-optimization-of-model-harnesses.md) searches harness code with a general agentic proposer and a trace filesystem. This paper trains the proposer itself to carry a reusable revision procedure across task families. Code remains the adapted state; learning improves the editor before deployment.
- **Routing evidence is a practical lesson.** Preserve original evidence for answer/verification calls while using summaries to steer retrieval. This is different from retaining every observation in every call. It complements [the coding harness study](empirical-study-harness-design-coding-agents.md): compact runtime context and keep raw traces available to the engineering/verification consumer; neither paper establishes that one representation suits all consumers.
- **Test learned edits against a strong fixed scaffold first.** The 0.69 tool-loop baseline prevents reading “better editor” as “best harness.” Evaluate held-out outcomes, validity, solver/retrieval work and feedback budget alongside proposal quality.
- **Keep promotion checks independent.** [Prime Agent](prime-agent-self-improving-rlm-harness.md) and [RSIAgent](rsiagent-autonomous-exploration-recursive-self-improvement.md) show locally rewarded mistakes becoming reusable state. Harness learning uses screening and separate questions, but [Reality Is the Final Verifier](../agentic-engineering/reality-is-the-final-verifier-two-gap-framework.md) still applies: benchmark success does not prove the revised program respects deployment requirements.

Source: [arXiv:2609.35738v1 PDF](https://arxiv.org/pdf/2609.35738v1), all 36 pages read, including references and Appendices A–F, 2026-10-12. Immutable PDF and layout-text extraction archived in `pdfs/2609.35738v1-harness-learning.{pdf,txt}`. Adjacent works in the paper's comparison table are reported as the authors' descriptions, not independently ingested here.
