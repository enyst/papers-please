---
title: "Mind Your HEARTBEAT! Claw Background Execution Inherently Enables Silent Memory Pollution"
authors:
  - Yechao Zhang
  - Shiqian Zhao
  - Jie Zhang
  - Gelei Deng
  - Jiawen Zhang
  - Xiaogeng Liu
  - Chaowei Xiao
  - Tianwei Zhang
arxiv_id: "2603.23064"
arxiv_url: "https://arxiv.org/abs/2603.23064"
published: "2026-03-24"
updated: "2026-03-25"
source: "arXiv"
project: "memory"
scope_note: "pass-three security include"
agent_setting: "personal AI agents with heartbeat-driven background execution and shared memory between background and foreground tasks"
memory_mechanism: "Shows how ordinary background content exposure can silently pollute short-term and then long-term memory, later altering foreground behavior."
icl_relevance: "medium"
tags:
  - agent-memory
  - security
  - memory-pollution
  - background-execution
categories:
  - cs.CR
  - cs.AI
  - cs.SI
---

- **One-line take:** A strong warning that memory pollution can happen even without classic prompt injection if background execution shares the same memory path.
- **What it stores:** Short-term session context and long-term agent memory that may absorb misinformation from unattended background channels.
- **How memory is used at inference time:** Shows how ordinary background content exposure can silently pollute short-term and then long-term memory, later altering foreground behavior.
- **Why it matters for this sub-project:** Important because it expands the security story from adversarial prompting to ordinary background misinformation and provenance failures.
- **Caveats / limits:** The findings are tied to a specific architectural pattern in Claw-like agents, so transfer to other designs requires care.
- **Abstract-level summary:** We identify a critical security vulnerability in mainstream Claw personal AI agents: untrusted content encountered during heartbeat-driven background execution can silently pollute agent memory and subsequently influence user-facing behavior without the user's awareness. This vulnerability arises from an architectural design shared across the Claw ecosystem: heartbeat background execution runs in the same session as user-facing conversation, so content ingested from any external source monitored in the background (including email, message channels, news feeds, code repositories, and social platforms) can enter the same memory context used for foreground interaction, often with limited user visibility and without clear source provenance. We formalize this process as an Exposure (E) $\rightarrow$ Memory (M) $\rightarrow$ Behavior (B) pathway: misinformation encountered during heartbeat execution enters the agent's short-term session context, potentially gets written into long-term memory, and later shapes downstream user-facing behavior. We instantiate this pathway in an agent-native social setting using MissClaw, a controlled research replica of Moltbook. We find that (1) social credibility cues, especially perceived consensus, are the dominant driver of short-term behavioral influence, with misleading rates up to 61%; (2) routine memory-saving behavior can promote short-term pollution into durable long-term memory at rates up to 91%, with cross-session behavioral influence reaching 76%; (3) under naturalistic browsing with content dilution and context pruning, pollution still crosses session boundaries. Overall, prompt injection is not required: ordinary social misinformation is sufficient to silently shape agent memory and behavior under heartbeat-driven background execution.
