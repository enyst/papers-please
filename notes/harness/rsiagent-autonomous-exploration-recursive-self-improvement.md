---
title: "RSIAgent: Autonomous Exploration for Recursive Self-improvement in New Environments"
authors:
  - Sibo Zhu
  - Shicheng Fan
  - Xinyue Wang
  - Wenyi Wu
  - Kun Zhou
  - Biwei Huang
published: "2026-09-14"
source: "arXiv:2609.15364 (cs.AI); UC San Diego · University of Illinois at Chicago"
arxiv_id: "2609.15364"
arxiv_url: "https://arxiv.org/abs/2609.15364"
mechanism: "A curriculum / actor / verifier trio autonomously explores an unfamiliar environment — broad parallel practice first, then targeted deep practice — grounds each outcome in environment evidence, consolidates verified experience into a memory bank, freezes it, and reuses it at test time with no weight updates."
read_depth: "full"
tags:
  - harness
  - self-improving
  - recursive-self-improvement
  - memory
  - computer-use
  - multi-agent
  - exploration
  - training-free
---

# RSIAgent: Autonomous Exploration for Recursive Self-improvement in New Environments

- **One-line take:** adaptation to a new environment by *exploration plus verified memory
  construction*, measured — frozen memory lifts strong open models above frontier closed ones on
  OSWorld 2.0 and Agent's Last Exam without touching a single weight, and the paper's own failure
  analysis shows exactly how that loop poisons itself.

## The setup

Digital agents meet environments whose interfaces, tools and failure modes are not in their
pretraining. Adapting by collecting more data and training is expensive and awkward in private or
fast-changing environments. RSIAgent is the training-free alternative: build the environment
knowledge yourself, verify it, and reuse it.

The formal shape is worth keeping: the agent acts on a task `q` conditioned on a **durable memory
`M`** and the interaction history `h_t`, while `M` **persists across tasks** even though `h_t`
resets. Actions are code (`code-as-policy`), so the same interface drives GUI applications.

## Mechanism

**Three roles, separate contexts (a "multi-agent harness framework"):**

- **Actor** — the policy model, equipped with an *evolvable* memory of environment knowledge,
  reusable procedures and scripts, and failure lessons. After a verdict, the actor consolidates
  the grounded experience and carries the updated memory into subsequent instances.
- **Verifier** — an independent evaluator that inspects environment feedback (execution results,
  interface states, observable evidence) rather than the actor's account. Its context is isolated
  from the actor's private reasoning and memory, to reduce correlated errors.
- **Curriculum** — decides what to practise next: prerequisite skills, informative variants,
  failure-driven practice, stress-test cases. It stops when new tasks are unlikely to add
  knowledge.

**Two stages, broad then deep:**

1. **BRS (Broad Recursive Self-exploration)** — parallel waves of diverse practice. The nominal
   budget is 8 exploration projects with up to 4 concurrent; each wave starts from the *same
   immutable memory snapshot* and cannot see sibling work.
2. **DRS (Deep Recursive Self-exploration)** — sequential, increasing difficulty, one verified
   consolidation before the next curriculum decision, aimed at hidden constraints, boundary
   conditions and unknown causal dependencies.

Then **memory is frozen** and reused: curriculum agent and all memory updates are disabled at test
time, and the actor just reads the procedures, constraints and lessons.

**Memory governance — the part I'd steal, in detail:**

- *Experience-owned learning.* The actor that produced an experience decides what to keep from it.
  Two steps: **distillation** (extract procedures, constraints, failure lessons) then
  **reconciliation** (check the new entries against older ones, revise contradictions, qualify
  unsupported conclusions).
- *Canonical memory ownership.* Only *completed* actor learning is promoted to the memory bank.
  Work-phase edits are discarded first; the actor receives the current canonical memory at the
  update boundary; the curriculum agent works on a **disposable copy** and its edits are never
  synchronized back; neither the curriculum agent nor the verifier approves memory wording.
- *Parallel work, sequential updates.* A wave runs concurrently, then the original actor contexts
  resume one at a time in the order the curriculum agent authored, each update building on the
  latest canonical memory including earlier updates from the same wave.
- A *learning diagnosis* — conclusions and uncertainties — travels to the curriculum agent
  without passing the actor's private reasoning transcript.
- Verification uses reset-and-replay or checkpoint restoration so the verifier's probes cannot
  mutate the submitted artifact. `UNVERIFIED` is a real outcome: an unresolved case is neither a
  success nor a failure learning example.

## Results

- **OSWorld 2.0 (0808 offline, 82 tasks):** partial 71.97 → **78.98**, binary 37.80 → 42.68 with
  RSI on vs off. **Agent's Last Exam (Near-term, 67 tasks):** partial 83.75 → 84.82, binary
  49.25 → 50.75.
- Beats the reported GPT-6 Astra scores by 6.38 and 2.56 points on partial score, and beats
  Claude Opus 5 on both benchmarks — using GLM-5.3 as actor and Kimi-K3 as verifier/curriculum.
  (For scale: GPT-6 Astra reports 72.60 / 82.26 partial on those two.)
- **Ablation (4 OSWorld tasks):** full RSI 74.54 mean partial vs broad-only 65.52 vs deep-only
  56.50. Broad-only beat the baseline on every task; **deep-only fell below the baseline on two
  tasks** — targeted practice without breadth can make things worse, and breadth alone leaves the
  hard cases unresolved.
- **GameCraft-Bench (40 sampled tasks, four generator models):** RSIAgent beats the Play2Code
  continual-improvement baseline in every block (e.g. Qwen3.8-27B generator: 41.30 baseline →
  47.67 Play2Code → 57.46 full RSI).
- Per-task curves show **discrete jumps**: memory accumulates gradually, then a remaining
  bottleneck is resolved and the score steps up (T044 video editing 100%, T065 railway booking
  100%, T049 presentation repair 80% by step 8).

## Failure modes — the most useful section

Three mechanisms, and they interact so an early mistake persists *through practice*:

1. **Insufficiently targeted exploration.** Practice that never challenges the decision
   responsible for a weakness leaves the wrong rule in memory. Their example: the curriculum
   generated document processing and submission persistence, but never tested obtaining
   unavailable user information — so the bad missing-information rule stayed.
2. **Incomplete verification.** The verifier returned PASS despite unsupported field values or
   artifact discrepancies under the official rubric. "Checking that an intended output was
   produced does not establish that the underlying interpretation or requirement checklist was
   complete." An accepted mistake then becomes the basis for future memory updates and
   exploration.
3. **Unreliable memory consolidation.** A rule like "the missing-data marker is a valid answer"
   or "unavailable information is a negative answer" gets retained and reused without ever
   fetching the missing fact. Their conclusion: **memory must preserve the conditions and
   uncertainty of an experience, rather than treating local acceptance as evidence of general
   validity.**

## Honest caveats

- RSI costs extra test-time compute by construction, and results depend on finite exploration
  budgets, stopping policies and the quality of the learned memory.
- The verifier is model-based, so its errors propagate into later exploration and memory updates
  (their own failure mode 2 is this happening).
- "Open-source beats closed-source" is measured on one configuration pair (GLM-5.3 actor,
  Kimi-K3 verifier/curriculum) on two benchmarks, with baselines mostly copied from official
  reports — not a like-for-like harness comparison.
- Tasks without a completed RSI result keep their baseline score in the aggregate; the paper
  states this, and it means the headline gain is partly a selection effect.
- Their own limitations section admits the experiments do not isolate every component's
  contribution, and different environments may need different tools, verification signals and
  exploration strategies.

## Why it matters for us

- This is our own dream/heartbeat loop's shape, measured: a curriculum decides what to practise,
  a verifier grounds the outcome, memory keeps what survived. RSIAgent gives us numbers, a
  comparison arm, and — more valuable — **an audit of how that loop fails**.
- Failure modes 2 and 3 are directly portable to SmolPaws' memory practice, and they match
  lessons we already hold in weaker form: grounding beats self-report, and a locally accepted
  result is not a general rule. Their fix is concrete: keep the conditions and the uncertainty
  with the entry, not just the conclusion.
- The **explore-then-freeze** split (writes allowed during the exploration phase, read-only at
  execution time) is a clean separation we could copy for any environment-specific knowledge —
  it also bounds the blast radius of a contaminated rule to one phase.
- The wave/update discipline (parallel acquisition, sequential canonical updates, disposable
  copies for non-owners, one owner per memory) is a workable answer to "who is allowed to write
  memory", which we have been circling in the consolidation discussions.

Source: [arXiv:2609.15364](https://arxiv.org/abs/2609.15364) (read full HTML, 2026-09-17).
