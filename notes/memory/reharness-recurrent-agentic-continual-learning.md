---
title: "Recurrent Harness for Agentic Continual Learning"
authors:
  - Yuxin Xiao
  - Zhiyun Lu
  - Jianyu Wang
  - Yangtian Zhang
  - Yang Song
  - Qifan Wang
  - Bailin Wang
published: "2026-10-08"
source: "arXiv v1"
arxiv_id: "2610.12668"
arxiv_url: "https://arxiv.org/abs/2610.12668"
source_pdf: "../../pdfs/2610.12668v1-reharness.pdf"
read_depth: "full"
read_date: "2026-10-19"
memory_mechanism: "After a task, use its feedback to revise retrieved reflections against their original source trajectories, then write a new reflection using those revisions as demonstrations; keep model weights fixed."
tags: [agent-memory, harness, continual-learning, backward-revision, source-grounding, distribution-shift, reflection, cost]
---

# ReHarness

**One-line take:** feedback should repair the old lesson that misled the agent, as well as produce a new lesson. Keep the old lesson grounded in its own evidence: discovering that one interpretation failed does not prove an untested alternative.

## Exact update loop (§§2–3; Appendix prompts)

- Store reflections **and their original raw trajectories**. Retrieve five by Qwen3-Embedding-8B similarity between the current query and each source query. Raw-context baselines use the same retrieval basis where applicable.
- **Forward read:** solve the next instance using retrieved reflections. Record actions, observations, outcome and reward; hidden model reasoning is excluded from stored trajectories.
- **Backward revision:** revise each retrieved reflection separately using the old reflection, its original trajectory and the just-completed trajectory. The new trajectory diagnoses misleading generalization or matching conditions. The **original trajectory remains the sole source of factual content** for that old reflection. Non-retrieved reflections remain unchanged.
- **Forward write:** produce a new reflection from the current trajectory, with revised reflections as demonstrations of style and complementary perspectives. Prompts separate operational evidence from interpretation and explicitly prohibit fabricated novelty.
- No parameter gradient, held-out validation or counterfactual replay in the main method. “Backward” means revision of textual state, not backpropagation through weights. Keeping old source trajectories is necessary; this does not eliminate raw-history storage.
- Memory persists across instances within a stream and resets between streams. Models are Claude Opus 4.8, GPT-5.5 and Gemini 3.7 Flash with high-thinking defaults.

## What they measure (§§4–5; appendix tables)

- **16 tasks:** CL-Bench's six shifting multi-round environments (12–120 instances); MemoryBench's five English writing tasks with sequential feedback (17–47 instances); MemoryArena's five domains with interdependent tasks. Three seeded rollouts per configuration start from matched initial conditions, then evolve independently.
- Score is **normalized gain** `(method − stateless)/(maximum − stateless)`, not accuracy or percentage-point improvement. Average across the nine benchmark–backbone cells: ReHarness **0.240**, Top-K raw context **0.168**, Full raw context **0.164**, Mem0 0.131, online GEPA 0.092, DoT 0.071, ACE 0.043 and ReflectionBank 0.034.
- Best or tied in **8/9 aggregate cells**, not every task: Gemini CL-Bench Full raw is 0.234 versus ReHarness 0.233; GPT MemoryArena ties Full raw at 0.358. Paired task-stream Wilcoxon comparisons with Bonferroni correction report adjusted p=0.039 versus Top-K and 0.043 versus Full raw.
- **Ablations on Claude CL-Bench:** full 0.217; remove backward revision 0.144; omit revised-reflection demonstrations 0.191. Counterfactual replay reaches 0.335 but retries the completed instance; authors explicitly distinguish this from the valid streaming protocol.
- Post-shift stability/plasticity averages: ReHarness **0.015/0.241**, Full raw 0.010/0.232, Top-K 0.003/0.205. Stability concerns the first post-shift instance before its feedback; plasticity concerns later adaptation. Per-backbone results vary. Noisy poker rewards provide weak credit assignment and little or negative gain.
- Retrieval sensitivity: k=5–20 generally works better than much larger retrieval sets; k=5 is the main setting. This is a post-hoc sensitivity result, not a learned retrieval policy.

## Grounding audit and useful failure cases

- GPT-5.6-Sol audits atomic revised claims: **95.3/98.7/96.3%** source-entailed across the three backbones; later-trajectory leakage **2.1/0.8/1.3%**; unsupported **2.6/0.5/2.4%**. Grounding is prompt-enforced and model-judged, not a mechanical guarantee; leakage is small but nonzero.
- **Spectrum:** an early reflection inferred an unseen transmitter grid and recommended inventing channels. Later use worsened reward. Revision recast gap-filling as unsupported speculation and favored actually observed peaks. Subsequent behavior improved; this is an illustrative trace, not a separately randomized causal experiment.
- **Database:** getting the wrong answer with `prc_usd` does not establish that `prc/100` is correct. A bad reflection asserted exactly that. Revision retained uncertainty and advised checking all plausible price columns. A later `prc_v2` observation belongs to the new trajectory, not retroactively to the old source. This is a useful distinction between correcting a rule and rewriting history.

## Token savings do not imply the cheapest system

| One Claude CL-Bench rollout | Input tokens | Output tokens | Total | Reported cost |
| --- | ---: | ---: | ---: | ---: |
| ReHarness | 37.19M | 4.38M | 41.57M | $254 |
| Top-K raw context | 52.20M | 0.46M | 52.66M | $85 |
| Full raw context | 141.68M | 0.44M | 142.12M | $314 |

- ReHarness reduces total tokens and beats Full raw on this cost comparison, but is roughly **three times the cost of Top-K**, largely because revision adds expensive output. Cache-aware pricing matters. This is one rollout/configuration, not a universal bill or latency claim.
- Feedback can improve the applicability of an old reflection without proving the reflection caused the current outcome. Noisy rewards and mistaken source interpretations remain risks. No security guarantee follows from source grounding; a source can itself be malicious.

## Why it matters for us

- Add a **repair path** to consolidation: find which retrieved lesson influenced a failure, reopen its source, and narrow or qualify it before adding more lessons. A lesson should state when it applies and distinguish observations from proposed explanations.
- Keep cross-episode synthesis separately linked to all contributing sources. ReHarness's old-source-only rule concerns revision of a single-source reflection; it does not prohibit legitimate new synthesis with explicit multi-source provenance.
- [LongHarness](../harness/longharness-stateful-evidence-management.md) addresses evidence→conclusion drift within a task; [Forgetting](../harness/scaling-discovery-requires-forgetting.md) addresses search-history anchoring across restart rounds. Combined lesson: retain audit evidence, revise interpretations, and deliberately choose the visible working set. See the [consolidation synthesis](../../wiki/memory-consolidation.md).

**Source:** [full v1 PDF](../../pdfs/2610.12668v1-reharness.pdf), all 20 pages including references, appendix tables, prompts and complete spectrum/database examples; [text](../../pdfs/2610.12668v1-reharness.txt). arXiv sidebar dates v1 October 8; manuscript header says October 12. Discovery: [DAIR.AI](https://x.com/dair_ai/status/2111862720446202052).
