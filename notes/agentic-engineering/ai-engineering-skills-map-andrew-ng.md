# AI Engineering Skills Map: Software Engineering Fundamentals — Andrew Ng

**Author:** Andrew Ng ([@AndrewYNg](https://x.com/andrewyng))
**Source:** [x.com/andrewyng/status/2093388974194872781](https://x.com/andrewyng/status/2093388974194872781)
**Date:** 2026-08-28
**Type:** Essay (part of a "AI Engineering Skills Map" series; more posts promised)

## One-Line Summary

The counterweight to the factory posts: even when an agent writes *all* your code, **human software fundamentals still matter** — not to type the code, but to *steer the tradeoffs* the agent would otherwise make blindly. "Developers who deeply understand how software works vastly outperform those who vibe code without understanding."

## The Core Argument

A novice who vibe-codes can ship simple apps, but the agent silently makes bad tradeoffs in latency, availability, consistency, reliability, maintainability, simplicity, cost — and the developer "didn't know such tradeoffs even existed." Fundamentals are what let you *know the tradeoffs exist* and steer toward the right ones for your context. Syntax memorization is obsolete; judgment is not.

## The Five Skill Areas (his map)

1. **Building full-stack applications.** Agentic coding pushes specialists (frontend, mobile) into broader full-stack roles. You still need to understand UI components, caching, page rendering, API choice/design, auth, state/session management, async processing, persistence, testing, security, accessibility.
2. **Managing data.** Singled out as *the* foundation — relatively hard to change even with agent-assisted migrations. Know access patterns → what to store and how long; right data models + storage type (relational / document / key-value / graph); transactions, concurrency, freshness, privacy/governance/compliance, lifecycle. Sharp line: **"if data architecture is chosen poorly, the AI doesn't know what it doesn't know."** Building data infra *for agents* (not just humans/traditional software) is a fast-evolving area.
3. **Designing system architectures.** Understand intent (users? latency? cost?) to choose platform, frontend/backend boundary, decomposition, state placement, monolith-vs-microservices, and the stack (sometimes via experiments). The right architecture is a **moving target by project phase** — prototype ≠ first production ≠ scaled.
4. **Making systems secure and reliable.** Testing strategy (unit/integration mix, frameworks, coverage); design around failure (rate limits, graceful degradation, minimize blast radius); **"shift left"** — security moves earlier; every dev is now partly a security engineer. Use AI to scan for vulns / supply-chain injections / cloud attack surface — but doing it well needs real security knowledge.
5. **Scaling and operating in production.** The full SDLC: deploy environments, release strategy, CI/CD, IaaS; observability, alerts, incident management; scaling (load-balancing, sharding, indexing, replication); plus version control, code review, dependency maintenance, tech-debt management.

## Why It Matters To Us

- **The human-skill complement to the factory/verification posts.** Lloyd/Uber/Yegge/poteto ask "how do we build and trust the machine that writes code?" Ng asks "what must the *human* still know to steer it?" Same era, orthogonal axis. Belongs in this dir precisely because it argues the factory doesn't remove the engineer — it *raises the abstraction* they operate at.
- **"The AI doesn't know what it doesn't know"** is the deepest line here, and it's a memory/context claim: the agent's input context is only as good as the data/architecture a knowledgeable human set up. Directly supports our view that context engineering (what the agent can see) is where the leverage is.
- **Tradeoff-steering ≈ verification's twin.** poteto says the bottleneck is verifying output; Ng says the prior bottleneck is *knowing which tradeoffs to demand in the first place*. You can't verify against a spec you didn't know to write. The two together: humans set the tradeoff targets, verification confirms they were met.
- **"Architecture is a moving target by phase"** echoes our own `prototype` vs. production skills, and the codebase-design/deep-module work. Validates keeping throwaway-prototype and production paths distinct.

## Where It's Thin / Skeptic's Notes

- **It's a curriculum, not a claim.** This is essentially a syllabus for DeepLearning.AI's skills map — comprehensive but uncontroversial. It lists what matters without a falsifiable thesis or evidence beyond "understanders outperform vibe-coders" (asserted, not measured).
- **"Fundamentals still matter" is the safe position.** Nobody serious disputes it. The genuinely open question — *which* fundamentals become vestigial as agents improve (he concedes syntax already has) — is the interesting part, and it's mostly deferred to "future posts."
- **Vendor gravity, softer.** Andrew Ng / DeepLearning.AI sell exactly the education this maps. The content is a public good; note it's also a course outline.

## Related

- `verification-and-trust-lauren-tan-poteto.md` — verification bottleneck; Ng supplies the "know the tradeoffs to verify against" prerequisite.
- `software-factory-uber-scale.md`, `software-factories-zach-lloyd.md` — the machine; Ng describes the operator's required knowledge.
- `notes/skills/` — this is a *human*-skills map; interesting contrast with agent-skill discovery.
- SmolPaws local: `codebase-design`, `prototype`, `improve-codebase-architecture` skills map onto areas 1–3.
