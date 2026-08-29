# Software Factory Design Patterns — AI That Works (Dex Horthy × Vaibhav Gupta)

**Speakers:** Dex Horthy (CEO/co-founder, HumanLayer) & Vaibhav "vaibcode" Gupta (co-founder, Boundary / BAML)
**Source:** [x.com/dexhorthy/status/2093452407808409786](https://x.com/dexhorthy/status/2093452407808409786) (video) · full ep on YouTube `tGbjIvvYuHE` (Boundary), **1:10:27**, 2026-08-28
**Transcript:** `transcripts/agentic-engineering/ai-that-works-software-factory-design-patterns.txt` (transcribed locally with Whisper `base` — ASR errors present; "BAML" often garbled, "buy" ↔ "by", "pie"/"amp" = PydanticAI/amp, "cloud/clawed" = Claude).
**Date:** 2026-08-28 · **Type:** Podcast / live workshop

## One-Line Summary

The **stack decomposition** of a software factory: break "agents build the thing" into ~5 composable layers — **compute → dev environment → inner harness → outer harness → control plane/orchestration** — each independently *buy-vs-build*. The thesis: as an engineer you should have **choice** — open interfaces to plug parts together, not go all-in on one vendor's full-stack cloud agent or build everything yourself.

## The Layer Stack (the core contribution)

| Layer | What it is | Buy-vs-build note |
|---|---|---|
| **Compute** | Where the agent runs (Boundary uses a pool of Mac minis/MacBooks; could be Daytona, a k8s/GCP cluster, Freestyle, etc.). | Easy to buy; Daytona/GCP/AWS SDKs are "already good" — don't wrap them. |
| **Dev environment** | Language runtimes, toolchains, ability to compile/test, web previews, **identity provisioning** (API keys, scopes, access to internal services). The "most controversial" layer. | Vaibhav's thesis: **you'll want to own this** unless you build "tiny toy Next.js apps." Real apps have 50+ shared services; forcing them into a vendor sandbox = friction (fake Linux kernels, missing syscalls, poking holes to reach shared infra). |
| **Inner harness** | The core agent loop — Claude Code / Codex / amp / Devon / Factory / OpenCode / PydanticAI. | Buy a "thick" one (ships browser, testing) or build a thin one and add your own. |
| **Outer harness** | Your customizations on top: **skills**, "why-loops" (e.g. drive-to-completion), MCPs, the stuff that makes it *yours*. | Where **compounding engineering** lands (see below). |
| **Control plane / orchestration** | "Most interesting and underserved." Dispatch work, view session traces/plans/architecture docs, cron/webhook triggers, PR-shaped review (not necessarily on GitHub), **permissions/audit, spend/budget**, and a database/dispatcher. | Nearly everyone builds their own — see "why no OSS control plane." |

Key framing: **understand the layers → make buy/build decisions per layer based on your needs.** You don't have to go all-in on the cloud stack (Cursor Cloud/Cognition), the Codex stack, or roll everything yourself.

## Boundary's actual in-house factory (the concrete example)

- **Compute:** pool of Macs; each runs the full toolchain (e.g. specific Rust version) + inner harness (CC/Codex) + outer harness (skills). GitHub auto-merge lets some loops be pure web.
- Each Mac runs a **local web server (REST API)**, exposed via a tunnel ("behaves like a remote server").
- A **cloud dispatcher web server** (own hosting) receives webhooks from **Slack, Linear, GitHub**, holds the DB, and routes work to the Macs = the **orchestration layer**.
- **Pets vs. cattle:** their Macs are currently *pets* (download a repo + run a script to provision; no one-button add). Cattle = on-demand, script-provisioned, disposable (like PR web previews). Acknowledged as the direction, but "you can get very far" with pets.

## The Feedback → Issue → Fix Loop (their bug factory)

Sharp, reusable pattern (nearly identical to poteto's Benny):
1. **Distrust all user feedback** — "you can't trust any feedback ever." First auto-check if it's *already fixed on latest*; if so, notify the reporter instantly.
2. **Spend your own tokens to build a really good repro.** "Issues are created *post-feedback*, not from feedback." If the agent can't produce a clear repro → **assign a human**. (Explicit rule at the top of their prompt: "for issues with clear code repros" this works; hard-to-repro needs something else.)
3. **De-dup is buggy** — no good de-dup agent exists; if it de-dups half, that's already a win. Everything carries a **confidence percentage** (some things will be wrong at some cadence; flaky issues fool "already fixed" checks).
4. Constantly re-check **every issue against every PR** — cheap CPU-time verification, no browser needed for most.

## Compounding Engineering (the memory idea)

"If all your engineers are yelling the same thing at Claude/Codex all day, how do you incorporate that into your outer harness?" A team-wide **memory system** that folds recurring corrections back into skills/the outer harness. (Same family as skills-from-traces — Uber, poteto, our dreaming.)

## On Interfaces / Why There's No Standard (the honest part)

- **ACP** (agent↔UI/editor protocol) is too narrow; **AG-UI** broadcasts events but neither supports **hooks** — the thing that would let a control plane lifecycle a harness and react to its events.
- Why no standard: **every harness is its own bespoke UI.** Claude Code / Codex / PydanticAI / OpenCode all have different (or no shared) hook models. "This is where all these things die." Rightfully so — harnesses have genuinely different tradeoffs (CC: "bring it, it's good"; PydanticAI: configure everything, more control, more to build).
- Analogy: web needed React's **"state is all you need"** insight to tame it; agent orchestration doesn't have its equivalent yet. Boundary/HumanLayer make money partly by *wrapping every harness* to plug in cleanly.
- **Don't wrap good interfaces with other interfaces** (old Sprout rule). Compute SDK tried to abstract clouds, "became a benchmark instead of an SDK"; at scale you're a GCP shop or an AWS shop and the native SDK is fine.
- **Why no OSS control plane:** code is so cheap to write now that no one wants someone else's control plane *unless* it comes with all the integrations (Slack + GitHub + your CLI) built. HumanLayer owns orchestration with a **swappable harness**; OpenInspect is OSS-full-stack-bring-your-compute. Boundary just builds the 2 layers they care about because "it's so easy to build now."

## The Meta-Bet (closing)

**"The browser wars" for harnesses.** Owning the browser was worth a lot; owning mobile was worth a lot; "a lot of people are betting that owning the harness is going to be worth a lot of money." Sign of it: Claude won't support `AGENTS.md` — insists on `CLAUDE.md` — "because they want CLAUDE.md to be the Claude thing... they're special." If harnesses don't play nice, they'll keep breaking each other's APIs. HumanLayer's stance: serious customers "prefer a good interface on top of compute and dev environment **that they own**."

(Bonus cold-open: riff on the FT article about OpenAI/Codex taking enterprise share from Anthropic — framed as consumer-brand vs enterprise-brand dynamics. Not the substance of the ep.)

## Why It Matters To Us

- **This is the missing engineering-diagram for the whole directory.** Lloyd/Uber/Yegge say "build a factory"; this decomposes *what a factory is made of* into layers you can reason about and own/rent individually. The clearest architecture artifact in the dir.
- **Directly maps onto OpenHands/SmolPaws.** OpenHands *is* an inner+outer harness + runtime (compute/dev-env); SmolPaws' skills = outer harness; the heartbeat/agent-server = a nascent control plane. Their layer names give us shared vocabulary for where the SDK sits and what's swappable.
- **"Own your dev environment" is a strong, contrarian claim** vs. the buy-everything cloud-agent pitch (Cursor Cloud/Cognition). For a local-first project like SmolPaws, it's validation: real toolchains + shared services resist full sandboxing.
- **The feedback→repro→verify loop is a concrete, adoptable design** — and it independently matches poteto's Benny almost step-for-step (distrust feedback, burn tokens on a good repro, human-fallback when no repro, cheap continuous re-verification). Cross-source convergence again.
- **"No hooks standard, every harness is bespoke"** is the honest counter to Yegge/Lloyd optimism: the interoperability layer that would make factories composable *doesn't exist yet*, and may not, because owning the harness is the prize.
- **Compounding engineering = team-scale dreaming.** Fold recurring human corrections into the outer harness — the multiplayer version of SmolPaws' nightly memory consolidation.

## Where It's Thin / Skeptic's Notes

- **Two founders describing their own products.** HumanLayer (orchestration) and Boundary/BAML (harness-wrapping language) both profit from exactly this "open interfaces / buy-vs-build" framing. The layer model is genuinely useful; the "you should own it" conclusion conveniently routes to their tools.
- **n=2, pre-cattle.** Boundary's factory runs on *pet* Macs with manual provisioning — they admit it's not yet the disposable/cattle ideal. It's a working setup, not a proven scalable one.
- **ASR caveat.** Transcribed with Whisper `base`; product names and quick crosstalk are garbled in places. Treat exact quotes as approximate — verify against the video before citing verbatim.
- **Vision vs. shipped.** "Compounding engineering," managed cloud sandboxes, thicker ACP — mostly described as coming/desired, not demonstrated.

## Related

- `software-factory-uber-scale.md` — production numbers for the same architecture; Uber's "four layers" ≈ this stack.
- `software-factories-zach-lloyd.md` — the factory *as concept*; this is the *as parts list*.
- `verification-and-trust-lauren-tan-poteto.md` — Benny ≈ their feedback→repro→fix loop, near-identical.
- `fences-not-sandboxes-steve-yegge.md` — another own-your-stack field report.
- SmolPaws/OpenHands local: inner+outer harness, skills = outer harness, agent-server/heartbeat = nascent control plane.
