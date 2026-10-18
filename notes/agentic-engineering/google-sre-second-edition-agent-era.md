---
title: "Google SRE, second edition: what changes in the age of agents?"
authors:
  - Betsy Beyer
  - David Huska
published: "2026-10-13"
source: "Google Cloud book announcement, with Google's separate AI-in-SRE engineering report"
url: "https://cloud.google.com/blog/products/devops-sre/sre-book-second-edition"
book_url: "https://sre.google/books/"
book_publisher_url: "https://www.oreilly.com/library/view/site-reliability-engineering/9798341607675/"
read_depth: full
scope_note: "Full announcement and separate public engineering report; the second-edition book itself was not read or acquired."
mechanism: "Apply reliability engineering to agentic operations through separate reasoning and execution controls, risk-dependent authorization, independent evaluation and production feedback."
tags:
  - sre
  - reliability
  - agentic-engineering
  - production-agents
  - actuation
  - independent-evaluation
  - incident-memory
  - book-bookmark
---

**One-line take:** Keep the rewritten SRE book as a reading target; Google's separate public engineering report already supplies concrete agent-era architecture: an agent proposes a production action, an independent control plane determines whether and how it may execute.

## The book: what is actually announced

- **Site Reliability Engineering, second edition** is described as a complete rewrite. Google's book page lists editors Betsy Beyer, Chris Jones, Christof Leng, David Huska, Jennifer Petoff and Niall Richard Murphy. The announcement is by Beyer and Huska, not a complete book-author list.
- **Operational updates:** user-centered/multi-tier SLOs, burn-rate alerting and automated error-budget policies; OpenTelemetry/traces and anomaly correlation; declarative platforms; continuous resilience checks and canaries; cloud cost/resource management; and hybrid SRE/platform teams.
- **AI has two roles:** running AI systems (GPU/TPU infrastructure, variable output/latency, training and data pipelines) and assisting operators (incident triage, postmortems, telemetry queries and predictive capacity analysis). These are topics claimed by the announcement, not independently checked chapter contents.
- **Access:** [official book page](https://sre.google/books/) and [O'Reilly listing](https://www.oreilly.com/library/view/site-reliability-engineering/9798341607675/). The official page links purchase options for the new edition; its existing free `sre-book/` contents link belongs to the older edition. No free second-edition full text was located in this check. O'Reilly returned 403 directly and through a reader; no book purchase or account access was attempted.

## The more concrete agent-era companion

- **Separate source, not a chapter:** [AI in SRE: How Google is Engineering the Future of Reliable Operations](https://sre.google/resources/practices-and-processes/ai-engineering-reliable-operations/), by Ioannis Papapanagiotou, Stevan Malesevic, Chris Heiser and Ruslan Meshenberg. The announcement's related [Cloud blog](https://cloud.google.com/blog/products/devops-sre/how-google-sre-is-using-agentic-ai-to-improve-operations) links this report through a short URL. No publication date is shown on the report; the fetched Cloud post is dated May 29, 2026. Retrieved versions may have evolved.
- **Separate investigation from permission to act.** AI Operator investigates alerts, draws on incident examples, chooses tools/skills and proposes mitigations. Actus, the actuation/safety control plane, turns proposals into concrete plans and enforces pre-flight checks. The reasoning agent does not receive unrestricted production-script access.
- **The checks have operational substance:** dry runs, an actual open-incident justification, capacity checks, concurrent-action checks and rate limits. Elevated risk can downgrade an otherwise autonomous action to a human-approved action. A central emergency stop can pause actions, block new ones or revoke autonomous permissions.
- **Distinct identities and least privilege:** agents use their own principals, not standing developer credentials. Permissions are granted on demand. Mutation tools enforce safety regardless of whether a person or an agent calls them. MCP is the interface, not the permission or safety boundary.
- **Autonomy is scoped and earned:** L1 assists investigation; L2 executes a human-approved plan; L3 can approve and execute bounded mitigations; L4 adds self-directed multi-step resolution. The report says AI Operator uses L2 for critical operations and L3 for minor incidents. It does not claim unrestricted L4 production operation.
- **Useful work can remain read-only.** AI Alert enriches alerts with linked evidence under an approximately two-minute budget. Incident Hypothesis suggests a credible cause and verification steps. Investigation Dashboards compose relevant evidence and domain-specific troubleshooters. These can reduce response time without granting mutation authority.

## Evaluation and operational memory

- **IRM-Analyzer reconstructs human trajectories** from chats, incident notes and commands. Incident history becomes both retrieval context and evaluation material. Bronze labels are heuristic, Silver labels are calibrated against human-verified Gold labels; stratified human review maintains the reference set.
- **Nightly evaluations combine two kinds of checks:** model judges assess investigation quality; deterministic scoring checks exact mitigation parameters against the reference action. “Roll back” is insufficient when the correct binary and version matter. Human verification still matters because incident records and inferred trajectories can be wrong.
- **Claims are narrower than a universal benchmark:** the report attributes a 10% reduction in mean time to mitigate to A/B-tested Incident Hypothesis assistance, and roughly 44% for Investigation Dashboards on supported incidents. It does not publish enough experimental detail here to reproduce these figures; do not add them together or generalize them to arbitrary agents.
- **Transparency needs traces, not faith in explanations.** The report exposes/logs agent reasoning and actions. Tool calls, inputs, policy decisions and observed effects support an audit; a model's plausible account of its reasoning alone cannot establish why it acted.

## What agent-written software changes

- **Humans review intent, architecture and policy**, while independent harnesses test and review implementation. Separation helps resist shared assumptions, but independent agents can still inherit the same incomplete requirements. Compare the [two-gap framework](reality-is-the-final-verifier-two-gap-framework.md).
- **Release validation must keep up with generation:** adaptive progressive rollout, production health checks and targeted feature flags. Faster code generation increases the amount of changed behavior to validate; it does not remove the reliability work.
- **Rollback can become less simple:** with many intervening changes, reverting a whole release may also discard unrelated security fixes. The report calls this the “Intervening Pull Request Problem” and advocates granular disablement and carefully controlled fix-forward. A generated patch still needs independent checks.
- **Preserve working deterministic automation.** The companion Cloud post explicitly says not to replace classical automation that already meets the need. The useful addition is handling unstructured evidence and variable investigations while keeping execution constraints enforceable.

## Why retain this here

- It extends the software-factory question from **who writes and reviews code** to **who authorizes and verifies its effects in production**. The compact transferable pattern is: observe → investigate → propose → independently authorize → act → verify → stop/escalate.
- For a small agent system, the first pieces worth borrowing are read-only diagnostics, narrow action APIs with dry-run, separate identities, bounded retries/cost, and a real emergency stop. A Google-sized platform is not a prerequisite.
- [Harness-of-Harness](harness-of-harness-multi-day-autonomous-development.md) separates implementation from evaluation; this source adds a separate production-actuation boundary. [Immutable artifacts](immutable-artifacts-josh-rosen.md) complement the action/authorization trace. Neither source's evidence substitutes for testing this architecture in a particular deployment.

**Reading scope and sources:** full October 13 [announcement](https://cloud.google.com/blog/products/devops-sre/sre-book-second-edition), full [companion Cloud post](https://cloud.google.com/blog/products/devops-sre/how-google-sre-is-using-agentic-ai-to-improve-operations), full public [AI-in-SRE report text](https://sre.google/resources/practices-and-processes/ai-engineering-reliable-operations/) and official book catalog page. Original HTML and extracted text archived under [`transcripts/agentic-engineering/`](../../transcripts/agentic-engineering/), retrieved 2026-10-18. Diagram images were not independently inspected; systems, incident datasets and performance claims were not audited. **The book is bookmarked, not read.** Discovery: [Geoffrey Huntley's post](https://x.com/GeoffreyHuntley/status/2111324796197785728), 2026-10-17; announcement text read via FxTwitter and archived.
