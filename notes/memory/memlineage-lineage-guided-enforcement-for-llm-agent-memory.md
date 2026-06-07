---
title: "MemLineage: Lineage-Guided Enforcement for LLM Agent Memory"
authors:
  - Ciyan Ouyang
  - Rui Hou
arxiv_id: "2605.14421"
arxiv_url: "https://arxiv.org/abs/2605.14421"
published: "2026-05-14"
updated: "2026-05-14"
source: "arXiv"
project: "memory"
scope_note: "pass-four include (Q2 2026 sweep)"
agent_setting: "LLM agents with persistent memory exposed to untrusted inputs"
memory_mechanism: "Attaches cryptographic provenance and LLM-mediated derivation lineage to every memory entry for enforcement at retrieval time."
icl_relevance: "medium"
tags:
  - agent-memory
  - security
  - memory-lineage
  - provenance
  - defense
categories:
  - cs.CR
  - cs.AI
---

- **One-line take:** Every memory entry gets a birth certificate — cryptographic provenance plus derivation lineage.
- **What it stores:** See memory_mechanism above.
- **How memory is used at inference time:** Attaches cryptographic provenance and LLM-mediated derivation lineage to every memory entry for enforcement at retrieval time.
- **Why it matters for this sub-project:** The strongest per-entry defense mechanism in the corpus — lineage tracking enables fine-grained trust enforcement.
- **Caveats / limits:** Newly published (Q2 2026); peer validation pending.
- **Abstract-level summary:** We introduce MemLineage, a defense for LLM agent memory that attaches both cryptographic provenance and LLM-mediated derivation lineage to every entry. Recent and concurrent work shows that untrusted content can be written into persistent agent state and re-enter later sessions as an instruction; the remaining systems question is how to preserve useful memory recall while preventing such state from justifying sensitive actions. MemLineage treats this as a chain-of-custody problem rather than a filtering problem. It is a six-module design around an RFC-6962 Merkle log over per-principal Ed25519-signed entries: a weighted derivation DAG records which retrieved entries influenced each new memory, and a max-of-strong-edges propagation rule makes Untrusted-Path Persistence hold for any chain whose attribution edges remain above threshold. The sensitive-action gate then refuses dispatches whose active justification descends from an external ancestor, while still allowing benign recall. We evaluate three defense cells against three memory-poisoning workloads on a deterministic mechanism-isolation harness; MemLineage is the only configuration in that harness that drives all three columns to zero ASR, while sub-millisecond per-operation overhead keeps it well below the noise floor of any LLM call. A Codex-backed AgentDojo bridge further separates strong-model behavior from defense-layer behavior: under an intentionally vulnerable tool-output profile, no-defense and signature-only baselines fail on all six banking pairs, while all MemLineage rows reduce strict AgentDojo ASR to zero. The core deterministic artifacts are byte-equal CI-verified; hosted-model AgentDojo and live-model sweeps are recorded as auditable logs rather than byte-pinned artifacts.
