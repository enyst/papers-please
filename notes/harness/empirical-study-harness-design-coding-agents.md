---
title: "An Empirical Study of Harness Design for Coding Agents"
authors:
  - Run-Ze Fan
  - Zihao Zhang
  - Simin Ma
  - Yebowen Hu
  - Shouju Wang
  - Kaiqiang Song
  - Fei Liu
  - Hamed Zamani
  - Xiaoyang Wang
published: "2026-09-17"
source: "arXiv v1"
arxiv_id: "2609.20804"
arxiv_url: "https://arxiv.org/abs/2609.20804"
source_pdf: "../../pdfs/2609.20804v1-empirical-harness-design.pdf"
read_depth: "full"
read_date: "2026-10-11"
mechanism: "Hold a LangGraph coding loop fixed and vary context-management policies across four window budgets, then ablate persistent planning and the workspace action interface at T4/128k; use paired task outcomes and trajectory annotations to explain model- and workload-dependent accuracy/cost effects."
tags:
  - harness
  - context-management
  - observation-elision
  - summarization
  - planning
  - action-space
  - coding-agents
  - ablation
  - trajectory-analysis
---

# An Empirical Study of Harness Design for Coding Agents

**One-line take:** choose scaffolding for the failure it prevents: context management mainly prevents overflow, a persistent plan helps weak models reach an edit and stronger models stop verifying, and a shell interface pays off only when the model can reliably use it. The evidence supports conditional harness design, not “more components” or “bash-only” as universal defaults.

## What they actually test (§§2–3)

- **Four models:** Nemotron-3 30B, 120B, 550B; Mistral-Medium-3.5-128B. The Nemotron sizes supply a within-family axis; Mistral tests a second interaction style. Model size is an imperfect capability proxy, not the causal variable they isolate.
- **Two benchmarks:** all 500 SWE-Bench Verified issues and 89 Terminal-Bench 2.1 tasks. SWE-Bench is Python-only; Terminal-Bench covers command-line work.
- **176 settings, not 176 tasks:** five context policies × four windows × four models × two benchmarks = 160; planning-off and bash-only at T4/128k add 16. Every setting runs once per task. This is **not a full-factorial study** of planning × interface × context policy × budget.
- **Fixed substrate:** ReAct loop on LangGraph, Harbor-owned task containers/verifiers, 300-step ceiling. Locally served BF16 models via SGLang; temperature 0, top-p 0.95, 16,384 output tokens per turn. Tool observations capped at 24k characters; up to eight read-only tools run concurrently.
- **Cost is token-priced, not an invoice or latency measurement.** They apply August 2026 OpenRouter input/output rates to local runs: $0.05/$0.20, $0.08/$0.45, $0.50/$2.20, $1.50/$7.50 per million tokens respectively. Serving hardware, deployment costs and cache economics are not established by these dollar figures.
- **Statistics:** task-paired, two-sided exact McNemar tests; Benjamini–Hochberg FDR 0.05 within comparison families. Stars in Tables 3–4 compare against the specified matched baseline; they do not establish that T4 beats every managed policy significantly.

## Context management: separate staying alive from thinking better

| Policy | Mechanism | Trigger |
| --- | --- | --- |
| T0 | No cross-turn compaction; stop on overflow | Window exceeded |
| T1 | Replace stale tool-output bodies with stubs | Hard threshold |
| T2 | T1 + external originals + `recall_event` | Hard threshold |
| T3 | LLM running summary, no elision | Hard threshold |
| T4 | Early elision + external originals; summarize only if still too large | Soft, then hard threshold |

- **Exact policy:** soft/hard thresholds are 0.60/0.85 of the usable window. Preserve system/task preamble and a recent window budgeted at 0.30, floored at two turns. Only compact the middle. The same model produces summaries in a separate tool-free call, updating an existing running summary (§2.3; Algorithm 1; Appendix A.3).
- **Overflow explains most of the large gain.** Mean managed-minus-T0 success gap on SWE-Bench falls from **35.7 points at 32k** to 15.9, 5.5, **2.7 at 128k**. Terminal-Bench: 9.5 → 7.5 → 4.8 → 2.8. Across models, T0 overflow falls from 78.7% to 8.7% on SWE-Bench and 61.0% to 12.1% on Terminal-Bench; all managed settings report zero overflow (§3.2, Figure 3).
- **The cheap baseline deliberately dies.** T0's low small-window cost partly buys failed, prematurely terminated runs. Compare success and cost jointly; low cost alone is not efficiency.
- **T4 wins on aggregate cost, not every cell.** Averaged over the four windows, T4 is cheapest among managed policies in seven of eight model–benchmark panels. Across all eight pairs it has the lowest average cost at each budget, comparable mean success, lower peak context and fewer summarizer calls than T3. Example exception: at 32k, Nemotron-3 550B SWE-Bench T3 costs $1.25 versus T4 $1.45 (Tables 3–4; Figures 4–5).
- **Recall availability did not produce reliable gains.** T2 versus T1: 15 wins, 14 losses, 3 ties; equal-weight mean difference **−0.36 points** (+0.40 SWE-Bench, −1.12 Terminal-Bench). Of 64 T2/T4 configurations, 36 never invoke recall; median call rate is zero. Mean calls/task across settings fall 0.540 → 0.069 → 0.011 → 0.007 as windows expand. All 16 additional planning/interface settings record zero calls (§3.2; Table 13).
- **Interpret the recall result narrowly.** The tool description explicitly offers re-reading files or re-running commands as alternatives. This tests optional event-ID recall in short-lived coding tasks with a reproducible workspace, not all retrieval or long-lived agent memory. Non-use can mean redundancy, failure to recognize need, or poor discoverability; these are not separated.
- **Missing clean ablation:** T4 contains recall as well as elision and summaries; there is no elision+summary-without-recall condition. T1/T2 establish the weak marginal result for recall without summaries; they do not prove recall can be removed from T4 unchanged.
- **Trajectory explanation:** at 32k, T0 runs often die in localization after roughly 20–30 median turns. Managed runs continue into edits/verification, largely preserving phase order. At 128k, tier differences in trajectory shape mostly shrink. Their evidence primarily shows improved execution survival, not improved reasoning quality (§4; Figures 32–39).

## Planning is persistent state plus stopping guidance

- **Intervention:** the model writes a complete todo list through `update_plan`; the harness stores it outside history and injects the current version before each turn. Prompt + first-turn reminder + repeated current-plan injection + tool are removed together in planning-off (Appendix A.2). This tests one persistent scaffold, not planning as an unrestricted cognitive strategy.
- **Weak-model benefit:** Nemotron-3 30B SWE-Bench success **13.6% → 25.2%** with planning; Terminal-Bench 8.99% → 13.48%. SWE-Bench median turns rise 5 → 40; no-edit termination falls **68.6% → 27.8%**. Extra cost buys reaching a repair attempt rather than abandoning localization (Tables 3, 6, 11–12).
- **Strong-model benefit:** Nemotron-3 550B SWE-Bench cost **$3.31 → $2.33** (about 30% less), success **67.8% → 65.8%**; Mistral cost **$4.65 → $3.14** (about 32% less), success **69.0% → 68.6%**. Most removed effort is post-edit verification, not localization or repair (§4; Figure 8).
- **Intermediate model is mixed:** Nemotron-3 120B planning raises SWE-Bench cost with lower success, but on Terminal-Bench reduces cost from $0.38 to $0.28 with the same 28.09% success. Do not infer a monotonic “bigger model → less planning” rule.
- **Practical distinction:** a plan can help by defining when to stop, even if it does not improve the patch. Keep required verification explicit; the paper reports small accuracy losses alongside lower cost and does not prove each removed verification was unnecessary.

## Action interfaces: capability and workload both matter

All figures below compare full tools versus bash-only, **planning on, T4/128k** (Tables 3–4).

| Model / benchmark | Full tools: success / cost | Bash-only: success / cost | Reading |
| --- | --- | --- | --- |
| Nemotron-3 30B / SWE-Bench | 25.2% / $0.09 | 10.2% / $0.03 | Cheap because many runs fail early |
| Nemotron-3 550B / SWE-Bench | 65.8% / $2.33 | 69.4% / $1.11 | +3.6 points, about 52% less cost |
| Nemotron-3 550B / Terminal-Bench | 44.94% / $2.43 | 50.56% / $1.70 | +5.62 points, about 30% less cost |
| Mistral / SWE-Bench | 68.6% / $3.14 | 45.4% / $1.72 | **−23.2 points**, serious regression |
| Mistral / Terminal-Bench | 37.08% / $2.22 | 43.82% / $2.75 | +6.74 points, **higher cost** |

- **“Bash-only” still has auxiliary tools:** `update_plan` and `recall_event` remain enabled. It means shell-only **workspace operations**, not a single-tool agent (§2.2).
- **Weak model's problem is interface adherence.** Nemotron-3 30B emits learned calls to tools absent from the bash-only registry; 66% of its bash-only Terminal-Bench trajectories terminate after out-of-interface emissions. Thus the result includes action-vocabulary alignment, not just difficulty writing shell commands (§3.2).
- **Strong shell model bundles work:** for Nemotron-3 550B, SWE-Bench tool calls fall 98.4 → 67.1, re-patches 4.6 → 1.5, median largest edit 18 → 54 lines. Terminal-Bench median actions fall 47 → 31; create/replace share rises 50.9% → 76.1% (Tables 7, 11). Larger composite actions reduce model–harness round trips.
- **Mistral supplies the counterexample.** With all tools it already uses bash for 71.9% of Terminal-Bench workspace actions, versus 40.4% on SWE-Bench. Under bash-only, SWE-Bench no-edit termination rises 1.2% → 32.8%; file-localization failures among unresolved runs rise 16.0% → 41.4%. Task type matters even at the same weights (§3.2; Tables 10, 12).
- **The comparison bundles safeguards.** Full file tools enforce full-read-before-write, external-change hashes, tracked file state and automatic Python diagnostics. Shell writes bypass that tracking/diagnostic path. Tool availability, instructions, validation and action granularity all change together; this is not a clean “fewer tools are better” test (§2.2; Appendix B.1).

## Appendix details that change the interpretation

- **Fixed anti-loop mechanism:** remind after five identical calls or identical failing calls; terminate after eight identical failing calls. Arguments must be byte-identical; changing a read offset ends a streak, and permission denials do not count as failures. The study does not ablate this mechanism (§2.4; Appendix A.4).
- **Summarizer preserves work state:** goal, files touched, done, pending, errors/fixes, current state, next step; exact paths/function names/errors/task IDs. Update a running summary, drop stale facts, preserve current ones. This is task continuation state, not biographical memory (Figure 18).
- **Full-read gate has operational cost:** paginated partial reads do not accumulate into the required `full_read=True` state. A read qualifies only with offset 1 and a limit covering the file. Bash writes are an alternate path, not subject to the same file-state mechanism (Figure 21–28).
- **Annotation quality has evidence:** GPT-5.5, high reasoning, temperature 0.6; three human annotators review disjoint splits of 200 trajectories / 15,610 units. Aggregate reported agreement about 94.2%, weighted κ 0.929; per-split Terminal-Bench agreement varies 79.8%–97.3%. These are human–judge checks, not human–human inter-rater agreement on common items (Appendix C.2).
- **Diagnosis differs from phase labeling:** unresolved SWE-Bench runs are assigned the earliest failure: file → line → patch → verification. The diagnostic judge sees gold-changed file names, the source patch and the final transcript portion. This is offline analysis with privileged evidence, not a deployable live failure detector (Figure 41).
- **Phase-label caveat:** SWE-Bench labels one dominant purpose per turn, Terminal-Bench labels individual actions. Figure 40 says a Fix must resolve the bug, but also prioritizes any source edit as Fix. That ambiguity affects interpretation of “no edit”; survival/profile evidence is descriptive rather than a clean mediation experiment.

## Limits and things not to overclaim

- **One run per task, two model families, two benchmarks.** Many 89-task Terminal-Bench differences are not significant after correction. No measured transfer to Claude/GPT/DeepSeek or general personal-agent tasks.
- **No planning/interface sweep at small windows.** The interactions most relevant to a constrained runtime are untested; their patterns at T4/128k are hypotheses elsewhere.
- **T0 means overflow termination, not sliding-window truncation.** “Context management helps” here is mostly a comparison against losing the task entirely. This does not establish summary faithfulness or performance over arbitrarily many compactions.
- **Aggregate efficiency is not universal dominance.** Lower token-priced cost can accompany accuracy loss; Mistral Terminal-Bench bash-only is more accurate but more expensive.
- **Minor source inconsistencies:** §3.2 rounds Nemotron-3 550B SWE-Bench bash cost saving to 53%; displayed dollars give about 52%. One figure annotates the Mistral drop as 24%, while Tables 3/10 establish 23.2 points; a sentence about its localization share is truncated. Use the tables for the numeric claims above.
- **Prompt mismatch worth checking in replication:** the shared summary wrapper says old content is recallable via `recall_event` even though T3 has no recall mechanism; `web_fetch` describes `web_search`, although search is excluded. These are documented prompt details, not evidence that either changed scores.
- No code/data release URL is supplied in the PDF. The extensive prompts/tables improve inspectability but do not substitute for running the implementation.

## Why it matters for us

- **A concrete condenser experiment:** compare stale-observation elision, summary-only, and staged elision→summary. Measure overflow, accepted task outcomes, peak input, summarizer calls and total tokens together. Treat the paper's 0.60/0.85/0.30 thresholds as a baseline to test, not magic constants.
- **Storage is not retrieval behavior.** OpenHands retaining an event log does not prove the agent will retrieve it. Measure recall demand and successful recovery, especially for non-reproducible evidence. The weak event-recall result challenges automatic claims about lossless storage, while leaving long-lived continuity and audit retention intact.
- **Plans can serve as stopping state.** Track whether a plan prevents abandonment or trims repeated verification; both can improve efficiency in different regimes. Keep verified milestones and stop conditions outside compressed conversation history.
- **Profile changes need harness evaluation.** The same action interface helps Mistral on repository repair and hurts its terminal success; a model swap warrants checking tool adherence, early termination and workload fit rather than blindly retaining the old scaffolding.
- **CodeAct's composition benefit has a boundary:** [CodeAct](../foundational/codeact-executable-code-actions-elicit-better-llm-agents.md) motivates executable composite actions. This study gives supporting evidence for a shell-capable model and a strong counterexample for blanket shell-only advice. CodeAct's Python action language and this bash interface are not identical interventions.
- **Keep raw traces for engineering, even if runtime recall is rare.** [Meta-Harness](meta-harness-end-to-end-optimization-of-model-harnesses.md) uses full traces to improve harness code; this paper measures a task-solving agent's optional recall. Different consumers, different objectives; no contradiction.
- **Context compaction is distinct from durable identity.** [Runtime-independent persistent agents](../memory/runtime-independent-persistent-agents.md) concerns continuity across deployments. This study concerns bounded coding trajectories. Do not use one benchmark's recall null result to discard the other substrate.
- **Success/cost does not settle safety.** [Reality Is the Final Verifier](../agentic-engineering/reality-is-the-final-verifier-two-gap-framework.md) keeps requirements and deployment assumptions in view. Shell efficiency here includes bypassing structured file safeguards; preserve security/validation boundaries when testing the idea.

Source: [arXiv:2609.20804v1 PDF](https://arxiv.org/pdf/2609.20804v1), all 43 pages read, including references and Appendices A–C, 2026-10-11. Local PDF and layout-text extraction are in `pdfs/`.
