---
title: "Object-Oriented Harness: Evolving Agent Harnesses through Object-Oriented Design"
authors: [Gaotang Li, Bhavana Dalvi Mishra, Yifei Ming, Yanfei Chen, Zhongying CuiZhu, Lesly Miculicich, Long T. Le, Rui Meng, Chun-Liang Li, Hanghang Tong, Chen-Yu Lee, Tomas Pfister]
published: 2026-10-20
source: arXiv
arxiv_id: "2610.28380"
arxiv_url: https://arxiv.org/abs/2610.28380
source_pdf: https://arxiv.org/pdf/2610.28380v1
mechanism: "Evolve specialized harness subclasses on discovery-task clusters, then route held-out tasks using frozen lessons and an observable base execution, retaining the base result when specialization does not fit."
read_depth: full
tags: [harness, self-improvement, inheritance, routing, generalization, execution-feedback]
---

**Take:** Preserve a base harness and evolve an inheriting family of targeted fixes. Execution-informed routing can improve heterogeneous tasks without forcing every task through the same changes; the evidence does not establish that inheritance alone causes all gains or that fewer selected-trajectory steps mean lower total inference cost.

## Method: specialize code, freeze the family, then route

- **Harness code, not model weights, changes.** Run the base on discovery tasks; retain source, trajectories, scores and reflections from successful and failed proposals. Group tasks by shared execution needs, not necessarily their application/domain. Clusters can split, merge or reassign tasks during search.
- An evolution agent chooses a cluster and a parent from the hierarchy, writes an executable subclass, overrides/adds methods and can call `super()`. It can alter prompts, tools, context management and completion checks; supported scaffolds also expose middleware, file backends and subagents. All methods execute in **one selected class instance**; ancestors are not separately running agents.
- Evaluate a candidate **directly on its target cluster**, without routing or rerunning every discovery task. Accept when its cluster score strictly improves and benchmark-specific checks pass; a judging agent handles ambiguous cases where configured. **No global non-regression requirement.** Rejected proposals remain available; repeated rejection lowers cluster priority. Enabled design/routing lesson stores summarize evidence; supplied lesson text is capped at 6,000 characters.
- A cluster's preferred harness and a subclass's source parent need not be the same. Parents remain available as inherited code; only active parents remain separate routing choices. This is code reuse plus a menu of specializations, not a universal “all ancestors are selectable” rule.
- **Test-time:** first execute the base, then route from the task, observable base trajectory, class applicability descriptions and frozen training lessons. Select the base → reuse its result. Select a specialist → run that class. No held-out grader scores, verdicts or hidden answers enter the router/executor. Hierarchy, lessons and model weights remain frozen across held-out tasks; this is not online self-modification.
- Router inputs vary: AutomationBench includes write/error counts and a bounded call/result digest; Workspace includes output extensions, dependency counts, persona/difficulty and execution counts; Toolathlon includes tool families and execution-error categories. The router has agent tools disabled. Automation uses a separate retrieval prompt before selection.

## Evidence and measurement boundaries

- **Splits:** AutomationBench **300 discovery / 300 held-out**; Workspace-Bench **288 / 100** (Lite-100); Toolathlon-GYM **251 / 252**. Automation and Toolathlon use deterministic task graders; Workspace uses task-specific agent-as-judge rubrics.
- Fixed executor **Gemini 3.5 Flash**; evolution agent **Claude Opus 4.8**, up to **40 iterations** per optimization method/benchmark. Main comparison says OO routing uses **Claude Sonnet 5**. Appendix A.4.2 also describes implementation defaults using Sonnet retrieval/Opus selection or proposer-model routing, plus overrides; the case study explicitly uses Opus for both. **Do not treat the defaults as proof of the exact main-run configuration.**
- Table 1 reports **mean ± SD over three executor runs**, not three independent evolutionary searches. Mean has different definitions across benchmarks: partial credit, micro rubric pass, mean reward. Strict PASS requires reward ≥0.999 or every rubric passed.

  | Benchmark | Primary metric | Base | OO-Harness | Strongest other method on that metric |
  |---|---|---:|---:|---:|
  | AutomationBench | Mean | 61.62 ± 0.15 | **77.41 ± 1.37** | AAH 75.40 ± 1.26 |
  | Workspace-Bench | Micro rubric Mean | 25.45 ± 2.98 | **39.48 ± 3.21** | AAH 38.62 ± 2.98 |
  | Toolathlon-GYM | Strict PASS | 31.15 ± 0.28 | **37.45 ± 0.98** | AHE 36.23 ± 1.19 |

- “Up to 15.79% absolute improvement” is **15.79 percentage points over base on Automation Mean**. Gains over the nearest competitor are much smaller. No significance test establishes superiority across these overlapping run distributions. Workspace strict PASS remains **8.33 ± 2.52%**, despite 39.48% rubric Mean; Toolathlon Mean **77.18 ± 1.15%** is distinct from strict PASS.
- Selected-trajectory steps fall **31.27→27.99**, **34.41→32.78**, **40.50→37.25**. **Steps excludes the base rollout used to route, other rollouts and auxiliary selection calls.** A specialist normally entails base execution plus specialization. Do not call this a total-token, latency or spend reduction.
- Parallel base best-of-2/5 and two-pass self-refinement use observable trajectories and no grades, but inference/model selection budgets are not identical to OO. Likewise, equal maximum search iterations do not mean equal training compute: cluster-scoped evaluations are deliberately cheaper than full-set evaluations. Figure 4 gives mean recorded search duration **109.1 h Meta / 29.0 h OO**, without a full cost-normalized frontier.

## Ablations: routing evidence and code reuse

- **Task-only vs task+trajectory router, same frozen catalogue:** Automation Mean **64.88→77.52**, Workspace Mean **40.03→40.56**, Toolathlon PASS **33.33→37.70** (Table 2, single runs, not the repeated main results). Execution evidence helps most when a fix targets an observed failure rather than a task's requested output format.
- Task-only routing uses self-reported applicability confidence ≥0.7; **this is not calibrated success probability**. Fallbacks differ by benchmark: Workspace's missing confidence defaults to one and invalid routes can invoke metadata fallback; other variants use zero/base behavior. The ablation compares implemented routing procedures, not a perfectly uniform confidence policy.
- **Inheritance ablation, Workspace, single independent search per variant:** Base-reset **29.39**, Flat **35.60**, OO **40.56** micro rubric. Base-reset retains diagnostic history but no evolved code; Flat copies accepted mechanisms into a class deriving directly from Base; OO inherits evolved parents and adds changes.
- All use the same initial tasks, clusters, base records, nominal budget and routing procedure. Flat/Base-reset keep shared helpers read-only; actual learned catalogues and routed assignments differ. **+4.96 pp OO over Flat supports that search organization here**, not a controlled swap of inheritance versus copied code with behavior held constant.
- In one Automation run, **134/300 (44.7%)** reuse base, 166 select specialists. Original base Mean is **77.15%** on reused tasks versus **44.40%** on specialist-routed tasks. This is a selection-conditioned diagnostic, not the causal benefit of rerunning those 166 tasks.
- **Extreme OOD:** evolve on 254 Toolathlon-GYM tasks, test on 49 original Toolathlon tasks with disjoint named application families. OO chooses **base for every test task**, retaining **59.18% PASS**; global Meta-Harness gets **44.90%**. This demonstrates successful abstention from inappropriate specialization on one selected split, **not positive transfer from learned subclasses**. No search/run variance is reported for this figure.

## Concrete changes worth understanding

- **File backend specialization:** writing UTF-8 text to `report.docx` does not create a Word document. The learned backend renders supported text as binary DOCX, can create a missing requested document from a draft, leaves existing targets untouched, and falls back to the parent on rendering failure. Valid file format still does not establish correct content.
- **Completion-check inheritance:** an ancestor requests another turn when a write-required task has made no mutating API call; its child adds a near-budget reminder when no write succeeded; another adds error-repair hints. These are runtime checks around a fixed executor, not new model knowledge.
- **Spreadsheet specialization:** a parent reminds the executor to save computed values rather than unevaluated formula strings. A child inherits context management and calls `super().verify_before_finish()` before checking saved percent-labelled cells. It can ask for one correction multiplying values strictly between zero and one by 100. **This assumes task-required percentage points** (20 rather than 0.2), not a universal Excel invariant; applying it to ordinary fraction-valued percentage cells could be wrong.
- **Refining an inherited intervention:** a child retains long-tool-output compression but bypasses compression after an early finish attempt. Inheritance can narrow a parent's trigger instead of only accumulating more rules.
- Routing lessons map repeated query-parsing errors to an API-error normalizer, missing service/resource information to a resource-manifest harness, and clean successful writes to base reuse. Lessons select interventions; they do not prove task completion.

## Limits and why it matters for us

- Single executor family and benchmark-specific scaffolds; no cross-model transfer study. Framework-only AHE and benchmark-grouped AAH are adaptations, not all original methods' deployment modes. Workspace rubric grading adds evaluator dependence. API outages, rate limits, permissions and interface drift remain explicit limitations.
- Rich trace metadata and an already-finished base run are useful but potentially expensive prerequisites. Production retries after a base run that performed writes need reset/idempotency semantics; the paper's benchmark routing result is not evidence that rerunning real side effects is safe.
- Training evaluations are cluster-local and repeatedly reused; unseen-task splits help but do not eliminate search overfitting or router misselection. No isolated lesson-store ablation establishes how much each lesson type contributes. Search acceptance details are benchmark-dependent, not a universal formal verifier.
- **For our harness design:** keep a stable base and narrow, testable extension points; attach applicability and contraindications to a learned change; route with observable evidence; retain a “leave on base” option. Measure **base + specialist + router** cost and downstream effects, not only the selected trace. The paper does not require turning the entire agent into a deep inheritance hierarchy.
- [Meta-Harness](meta-harness-end-to-end-optimization-of-model-harnesses.md) searches one global code artifact; OO adds shared-code specialization and explicit base reuse. [Harness Learning](harness-learning-generalizable-test-time-adaptation.md) instead trains a revision procedure; [RSIAgent](rsiagent-autonomous-exploration-recursive-self-improvement.md) emphasizes applicability/verification of consolidated behavior. Their mechanisms and evidence should remain separate.

Source: [arXiv v1 PDF](https://arxiv.org/pdf/2610.28380v1), full **20 pages**, references and Appendices A–B, read 2026-10-22. [Archived PDF](../../pdfs/2610.28380v1-object-oriented-harness.pdf) · [extracted text](../../pdfs/2610.28380v1-object-oriented-harness.txt). arXiv submission is dated 20 October; PDF header says 21 October. No experiments rerun or implementation repository audited.
