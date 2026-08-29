# Trust, Verification & Going Deep — Lauren Tan (@poteto) / pstack

**Author:** Lauren Tan ([@poteto](https://x.com/poteto)) — now Grok Bot @ xAI/SpaceX; prev Cursor, Meta, Netflix; React compiler core team.
**Primary sources:**
- Interview/workshop: ["How Cursor Turned AI Agents Into Better Engineers"](https://maven.com/p/e23d9c/how-cursor-turned-ai-agents-into-better-engineers), Maven w/ Colin Matthews, **2026-08-12**, ~60 min (chaptered).
- Written setup: ["How I Use Cursor"](https://x.com/poteto/article/2058975157503570132), 2026-05-25.
- Tool: **pstack** — her open-sourced skill set (`cursor.com/marketplace/cursor/pstack`, `/add-plugin pstack`).

**Date:** 2026 (interview Aug 12) · **Type:** Interview + practitioner essay + tool

> Note: the Maven page publishes a chaptered outline (see below); the full spoken transcript sits behind the video. The substance below is reconstructed from her written "How I Use Cursor" + the pstack skill list, which cover the same setup.

## One-Line Summary

Managing agents ≈ managing an engineering team of "new hires in a constant state of amnesia and idiocy": capable, teachable, but forgetful. You don't scale them by running many in parallel (breadth) — you scale by **building trust through rigor and verification** (depth). The bottleneck isn't generation, it's **verification**; solve that and a "dark factory for software" becomes possible.

## Interview chapter map (Maven, Aug 12)

Her setup, in her own ordering — a useful skeleton:
1. Agent Trust Curve: micromanagement → auto-merging PRs
2. Verification skills + **feature maps** for agents
3. pstack: skills to prevent agent hallucination
4. Maintaining skills using **evals + an eval playbook**
5. Scaling verification: local observation → cloud agents
6. Refactoring + setting guardrails
7. Managing PR sizes / structuring work
8. Strict CI constraints + the "Dune" architecture
9. Token usage, ROI, cost of agent-optimized codebases
10. Empowering product teams with GrockBot

## The Core Ideas

### 1. Depth-first, not breadth-first
"The value of orchestrating many agents in parallel comes from going deep, not broad." Naive parallelization "just makes them write slop faster." Go deep on one/few problems: best-of-N races, multi-model adversarial review, subagents of different models in one conversation. Running many CLIs in a GUI "misses the point" — the human-as-orchestrator is latent demand, not the goal.

### 2. Agents are amnesiac new hires
The load-bearing analogy (she's an ex-EM): new hires get onboarded to the codebase *and* to how work gets done; they arrive pre-trained with skills (debug, test, communicate). Agents lack persistence and learning, but you approximate it with **rules, skills, tools, long-term memory**. "Capable yet stupid, and very teachable." Failure modes = teaching opportunities.

### 3. Rigor as playbooks (pstack)
pstack encodes how experienced engineers actually work, as invokable skills. Heart is **`/poteto-mode`** — a higher-order skill that routes the right playbook for a task. Goal: "maximum impact with the least amount of code," not maximal LOC. Selected skills:
- `/architect` (settle types/data structures before crossing a function boundary), `/tdd` (failing test first), `/interrogate` (multi-model adversarial review), `/arena` (N parallel attempts, take best parts), `/why` (parallel evidence query across source control, issues, docs, chat, observability, errors, analytics), `/how`, `/unslop`, `/reflect`, `/figure-it-out`, `/show-me-your-work` (reviewable decision trail → committable TSV).
- **`/automate-me`**: mines your recent transcripts, drafts a personal "your-mode" skill from how you actually worked, routing through pstack underneath. (Self-improvement from traces — same idea as Uber's "auto-generate skill updates from traces.")

### 4. Trust is the unlock; verification is the bottleneck
"The bottleneck with agents is verification. Agents can write a large amount of code quickly. Making sure it's all correct is exceedingly difficult." And: **"Unless you can trust an agent to own a problem end-to-end, including verification, you cannot automate your processes."** Trying to parallelize agents you don't trust yet is "a huge waste of tokens and introduces more slop." Dial up trust → tackle more ambitious problems → eventually a "dark factory for software."

### 5. Benny / the maintenance factory
Her cloud-agent bot (Cursor automations, event-triggered e.g. on Slack messages): **triage** (reads image/video attachments, chats with reporter for repro steps, explores code with pstack) → **files a ticket** (correlating code, git history for regressions, Slack, Notion design decisions: "is it a bug or designed that way?") → **`/orchestrate`** recursively spawns agents → reproduces via *computer use* (cloud agents drive the desktop / CDP), fixes, subplanners spawn workers to **verify against the ticket**, others record before/after video + CPU traces/heap snapshots, a final worker opens the PR with the video in the description. "Fix bugs with confidence while I sleep."

## Why It Matters To Us

- **This is the missing operational layer under Lloyd/Yegge/Uber.** They describe factories; poteto describes *how you earn the right to build one* — the Agent Trust Curve. Her thesis "verification is the bottleneck; trust is the unlock" is the sharpest single sentence in this whole directory.
- **Skills-from-traces (`/automate-me`, `/reflect`) ≈ our dreaming + Uber's auto-skill-generation.** Three independent parties converged on "mine your own transcripts to improve your skills." Strong signal this pattern is real, not a gimmick. Directly validates SmolPaws' skills + dreaming design.
- **`/show-me-your-work` (committable decision trail) ≈ Rosen's receipts, lightweight.** A reviewable TSV of decisions is a poor-man's provenance graph. Same instinct: make the work auditable as a byproduct.
- **`/unslop` is literally our `no-ai-slop` skill.** And "maximum impact, least code" is SmolPaws' "if three lines work, I don't build an abstraction." Convergent values.
- **Depth-first > breadth-first** is a direct counter to the "spawn 50 agents" hype (cf. Yegge's 50-agent Wheelhouse). Worth holding these two in tension: Yegge goes wide *and* deep with heavy governance; poteto argues wide-without-trust is token-waste.

## Where It's Thin / Skeptic's Notes

- **Vendor-shaped, twice.** Written at Cursor, about Cursor, and pstack is a Cursor marketplace plugin; now she's at xAI shipping Grok Bot. The *ideas* (trust curve, verification bottleneck, depth-first) are portable; the tooling claims ("compaction is insanely fast in Cursor vs cc") are competitive positioning.
- **"Dark factory for software" is aspirational.** Benny is repeatedly flagged "still a work in progress." The end-to-end autonomous-maintenance loop is a vision with promising runs, not a proven steady state.
- **Trust curve has no metric here.** "Dial up trust" is qualitative. What *measures* readiness to auto-merge? The eval playbook is named but the actual gating criteria aren't public — same gap as Lloyd's "quality" hand-wave.
- **Amnesia analogy can over-promise.** "Long-term memory approximates a new hire" — but the memory/consolidation problem (see `notes/memory/`) is exactly what's unsolved. The analogy names the goal, not the mechanism.

## Related

- `software-factories-zach-lloyd.md`, `software-factory-uber-scale.md` — the factories her trust-curve makes possible; Uber independently does skills-from-traces.
- `fences-not-sandboxes-steve-yegge.md` — wide + governed vs. her deep + verified; hold in tension.
- `immutable-artifacts-josh-rosen.md` — `/show-me-your-work` as lightweight receipts.
- `notes/skills/` + `notes/memory/` — skills-from-traces and the amnesiac-agent memory problem.
- SmolPaws local: `no-ai-slop` (≈ `/unslop`), the dreaming loop (≈ `/automate-me`+`/reflect`), `handoff`.
