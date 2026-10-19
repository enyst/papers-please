---
title: "LongHarness: Advancing Agentic Reasoning over 100M-Token Corpora via Stateful Evidence Management"
authors:
  - Songtao Huang
  - Zhijie Zhong
  - Xiaohan He
  - Shuaiyu Zhang
  - Zhiyin Yu
  - Li Kang
  - Heng Zhou
  - Yutao Fan
  - Xiangchao Yan
  - Bo Zhang
  - Shiyang Feng
published: "2026-10-09"
source: "arXiv v1"
arxiv_id: "2610.13075"
arxiv_url: "https://arxiv.org/abs/2610.13075"
source_pdf: "../../pdfs/2610.13075v1-longharness.pdf"
read_depth: "full"
read_date: "2026-10-19"
mechanism: "Maintain source-linked evidence separately from conclusions and open gaps; use gaps to guide retrieval and explicit evidence revision/retraction to keep downstream reasoning current."
tags: [harness, evidence-management, provenance, long-context, working-memory, belief-revision, ablation]
---

# LongHarness

**One-line take:** separate what the agent read from what it currently believes, and make corrections operational. The paper shows useful gains from that separation, but still replays the complete interaction history: this is not a bounded-context replacement for history.

## Mechanism (§§2–3; Appendices A–B)

- **Three states:** interaction history H; Evidence Bank E with atomic, source-linked items; Conclusion State C with established conclusions, hypotheses and open information gaps. The next search should address a gap that could change the answer, rather than merely collect related text.
- **Acquisition:** document maps, BM25/regex search and bounded reads over Markdown documents. Search hits are navigation aids; source references become eligible for evidence only after a read exposes them. Sources include document/section/paragraph locators.
- **Evidence lifecycle:** upsert adds or updates supported material; revision creates a new ID and marks the old item superseded; retraction archives an item as inactive. Superseded/retracted evidence remains auditable. Batch writes can partially succeed; the agent must observe accepted changes before updating dependent conclusions.
- **Correction is not automatic truth maintenance.** The harness checks source locators and evidence-ID status, not whether a cited passage semantically entails the claim. It flags stale conclusion references but does not automatically rewrite dependent conclusions. Read/search can continue while a stale reference awaits repair.
- **Compute and final-answer checks:** declared evidence IDs must be active. This does not verify that every literal arithmetic operand came from those IDs, or that every conclusion has a valid dependency. The agent still chooses the facts and interprets them.
- **Critical context detail:** E and C are included every turn **alongside full H**, including reasoning and tool outputs. No history compaction/truncation is used; an oversized request that still fails after retries counts as an incorrect answer. The 100M tokens describe an external corpus, not one model context.

## Evaluation and results (§§4–5; Appendices C–E)

- **Tasks:** OfficeQA Pro V1: 133 questions over 697 Treasury documents (~100M tokens); V2: 90 questions over 1,435 documents with harder combinations. AA-LCR: 100 questions/234 supplied documents. LongBench v2 long subset: 108 questions, 132K–1.38M words per context, median 204K.
- **Backbones:** GLM-5.3-Flash and Qwen3.8-Flash. Same-backbone competitors include Claude Code 2.1.216, Codex CLI 0.135.0 and an RLM implementation. Direct OfficeQA reasoning receives BM25-selected context capped at 256K.

| OfficeQA exact match (%) | GLM V1 | GLM V2 | Qwen V1 | Qwen V2 |
| --- | ---: | ---: | ---: | ---: |
| LongHarness | 60.2 | 61.1 | 61.7 | 51.1 |
| Claude Code | 48.1 | 35.6 | 53.4 | 41.1 |
| Codex | 46.6 | 42.2 | 49.6 | 50.0 |
| Direct reasoning | 15.8 | 4.4 | — | — |

- LongHarness AA-LCR/LongBench-long: GLM **84.0/75.9%**; Qwen **87.0/76.9%**. The Qwen V2 advantage over Codex is only **1.1 points**, much smaller than the GLM result.
- Main tables use one run. Appendix D adds three GLM runs: V1 mean **59.90 ± 0.43** versus Claude Code 49.37 ± 1.57; V2 **59.63 ± 1.28** versus Codex 41.11 ± 4.00. These are reported standard deviations, not confidence intervals.
- **GLM ablations, V1/V2:** full 60.2/61.1; no persistent state 55.6/53.3; no evidence–conclusion coevolution 54.9/51.7; append-only evidence 56.4/51.1; no explicit gap guidance 55.6/53.3; generic notes 53.4/53.3. Revision/retraction matters beyond simply adding a scratchpad; removing it costs **10 points on V2**.
- **Conditional error audit:** GPT-5.6-Luna labels incorrect runs; correct answers automatically pass the first two stages. V2 evidence coverage is 87.8% versus Codex 76.7%; conditional evidence-editing success 87.3% versus Claude Code 84.6%; transformation success 79.7% versus Codex 70.4%. These stages are conditional and partly outcome-defined, not independent causal effects.
- **Arithmetic example:** a competing trace recognized a corrected 4,400 value but computed with 4,100. Its final 4,958.09 versus reference 4,962.46 fails exact match but passes 5% tolerance. This illustrates evidence drift, not a large numerical error.

## Limits and implementation implications

- LongHarness allows 200 steps, 60 searches, cumulative 1M read tokens and 16,384 tokens/read; model outputs are capped at 32,768. Other harnesses have different action semantics and RLM has 30 outer iterations/depth one. Same backbone does **not** mean matched inference compute or tool affordances.
- GLM median turns V1→V2 grow 22→30 for LongHarness, 21→116 for Claude Code and 19→43 for Codex. These are model turns, not equal-cost operations. The case study's 10 policy actions versus 170 shell calls is likewise not a latency comparison; total token and wall-clock efficiency are not established.
- **For our harness work:** test a small source-linked evidence ledger and separate provisional conclusions before building a larger memory subsystem. Give superseded entries stable lineage, and test whether dependent calculations actually stop using old operands. ID validation alone cannot ensure that.
- **Across papers:** [ReHarness](../memory/reharness-recurrent-agentic-continual-learning.md) repairs overgeneralized cross-task lessons; LongHarness repairs within-task evidence state. [Scaling Discovery Requires Forgetting](scaling-discovery-requires-forgetting.md) changes what history is visible while preserving an archive. These operate on different state layers; none justifies deleting provenance.

**Source:** [full v1 PDF](../../pdfs/2610.13075v1-longharness.pdf), including references and Appendices A–E; [extracted text](../../pdfs/2610.13075v1-longharness.txt). Discovered through [DAIR.AI's weekly collection](https://x.com/dair_ai/status/2111862720446202052).
