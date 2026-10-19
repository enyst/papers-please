---
title: "Scaling Discovery Requires Forgetting"
authors:
  - Shangyin Tan
  - Ben Zhou
  - Lakshya A Agrawal
  - Jialin Zhang
  - Yilin Chen
  - Qiuyang Mang
  - Donghyun Lee
  - Dennis Jacob
  - Koushik Sen
  - Alex Dimakis
  - Matei Zaharia
published: "2026-10-14"
source: "arXiv v1"
arxiv_id: "2610.20563"
arxiv_url: "https://arxiv.org/abs/2610.20563"
source_pdf: "../../pdfs/2610.20563v1-scaling-discovery-forgetting.pdf"
read_depth: "full"
read_date: "2026-10-19"
mechanism: "Periodically restart scored program-search agents from the best candidate while hiding prior session and candidate history; agents share evaluated candidate commits asynchronously and the harness retains the full archive."
tags: [harness, forgetting, context-management, program-search, multi-agent, test-time-scaling, anchoring, external-verification]
---

# Scaling Discovery Requires Forgetting

**One-line take:** fresh searches from the best verified artifact can outperform prolonged searches carrying their own failed attempts. “Forgetting” changes the agent's visible state; the harness still keeps the archive. Evidence comes from four closed-loop optimization tasks with one model, not general personal-assistant memory.

## What resets and what survives (§§2–3; Appendix A)

- Pi agents with **DeepSeek-V4.1-Flash** propose programs. A harness evaluates candidates after the agent stops and exposes score feedback; agents can edit files but do not own the scoring implementation.
- Compare one continuous agent, four independent parallel agents, and a four-agent communicating team with **three periodic resets/four rounds**. Match model-dollar budget in the main experiment.
- Team agents asynchronously share candidate Git commits and scores before the next proposal. No agent-to-agent chat channel; reading shared artifacts still consumes tokens.
- A reset starts a fresh session and resets the **visible workspace/candidate history** to the best candidate. It preserves the candidate, score and task instructions, not a summary of every failed experiment. Session and workspace reset together; the experiment does not isolate their separate contributions.
- The harness retains append-only candidate commits and session archives **outside the restarted agent's view**. This is neither destruction of provenance nor an instruction to erase safety constraints or user identity.

## Main evidence (§4.1, Table 1)

Three replicates per configuration. Values below are means ± standard deviation; Table 1 also gives best replicate. Figure 1 instead plots selected best runs.

| Task; model-spend budget | Single continuous | Four independent | Team + resets |
| --- | ---: | ---: | ---: |
| AHC014 rectangle construction; $20; score ↑ | 795K ± 210K | 964K ± 57K | 1,103K ± 50K |
| VLIW/SIMD kernel; $40; cycles ↓ | 1,426 ± 197 | 1,220 ± 44 | 1,097 ± 18 |
| FrontierCS Q171 grid optimization; $20; score ↑ | 64.0 ± 6.2 | 70.2 ± 1.1 | 80.8 ± 2.9 |
| nanochat training program; $20; validation BPB ↓ | 0.980 ± 0.003 | 0.980 ± 0.001 | 0.961 ± 0.012 |

- Best VLIW runs: 1,262 / 1,172 / **1,077 cycles** respectively. Best AHC014: 961,136 / 1,007,073 / **1,144,695**. Mean results support the pattern beyond the selected traces, but only three repetitions constrain uncertainty estimates.
- Authors report roughly **10%** average improvement over independent parallel search and **22%** over single-agent search; up to 15% and 39% respectively. These are relative task-performance comparisons, not accuracy-point gains on one unified metric.
- Evaluations: AHC014 over 30 cases; FrontierCS over 75; nanochat uses five-minute H100 training runs and held-out validation BPB. Dollar caps count **model inference spend**, not all evaluator/GPU costs. Do not treat this as matched total research compute.
- **Important confound:** the headline team condition adds communication and resets together. Its advantage alone does not attribute the whole improvement to forgetting.

## More direct forgetting test (§4.3)

- Start from the same AHC014 plateau prefix; allow **30 more proposals per agent**, either continuing history or restarting from the best candidate. Test single, independent-parallel and team settings, three repetitions each.

| Setting | Continue: gain / model cost | Forget: gain / model cost |
| --- | ---: | ---: |
| Single | 1.6 ± 0.2% / $6.66 | 4.5 ± 2.1% / $3.44 |
| Independent parallel | 1.9 ± 1.5% / $27.51 | 7.0 ± 3.3% / $13.97 |
| Team | 1.4 ± 1.3% / $24.67 | 9.2 ± 6.9% / $15.32 |

- This matched-prefix comparison better isolates resetting. It matches additional proposal count, **not additional spend**; reduced history also makes proposals cheaper. Unlike the main study, this intervention is only tested on AHC014.
- Across the main team runs, **32/36 resets** lead to a new best candidate, with gains generally shrinking in later rounds. Resetting is useful here, not guaranteed to improve every run indefinitely.

## Proposed explanation and limits (§§4.2–5)

- Authors diagnose history-induced anchoring and escalating verification. One VLIW single-agent run has **532/763 turns without a new candidate**, consuming 66.2% of model spend; 531 mostly read at most one file and declare a plateau. An asserted practical limit at 1,710 cycles was later beaten within the same run and by the team.
- After resets, the first ten turns contain larger edits (median 40 versus 6 lines) and less reasoning (2.9K versus 9.4K tokens). These traces support changed search behavior; they do not establish a model-internal psychological cause or show that every large edit helps.
- One model and four program-search tasks; three seeds; fixed periodic reset schedule. No evidence here that the schedule is optimal, that a reliable plateau detector exists, or that forgetting beats source-grounded summaries on all workloads.
- The best candidate is a compact, executable carrier of accumulated progress with an external score. Conversations, unresolved investigations and human preferences often have no comparable sufficient artifact. Forgetting their sources can lose the task itself.

## Why it matters for harness design

- Trial a **restart-from-verified-artifact** branch when optimization repeatedly reads/checks without proposing candidates. Keep a separate archive and preserve all instructions/constraints required for safe execution. Measure progress per dollar and evaluator cost, not only token count.
- Do not carry forward an unverified “this cannot improve” conclusion as if it were a constraint. Preserve the best artifact and evidence of its score; allow a fresh search to reconsider explanations.
- [ReHarness](../memory/reharness-recurrent-agentic-continual-learning.md) repairs a misleading lesson rather than hiding the whole search history; [LongHarness](longharness-stateful-evidence-management.md) keeps evidence and conclusions separate within a task. Together they suggest three independent controls: archived evidence, revisable interpretations and deliberately selected visible context. See [Memory Consolidation & Lifecycle](../../wiki/memory-consolidation.md).

**Source:** [full v1 PDF](../../pdfs/2610.20563v1-scaling-discovery-forgetting.pdf), all 14 pages including references, harness details and task prompts in Appendices A–B; [text](../../pdfs/2610.20563v1-scaling-discovery-forgetting.txt). Discovery: [DAIR.AI weekly collection](https://x.com/dair_ai/status/2111862720446202052).
