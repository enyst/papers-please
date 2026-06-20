---
title: "AlgoVeri: An Aligned Benchmark for Verified Code Generation on Classical Algorithms"
authors: Haoyu Zhao, Ziran Yang, Jiawei Li, Deyuan He, Zenan Li, Chi Jin, Venugopal V. Veeravalli, Aarti Gupta, Sanjeev Arora
arxiv_id: "2602.09464"
arxiv_url: https://arxiv.org/abs/2602.09464
published: 2026-06-03
venue: ICML
mechanism: Cross-paradigm benchmark for formally verified code generation (vericoding) across Dafny, Verus, and Lean
tags: [verification, formal-methods, code-generation, benchmark, dafny, verus, lean, vericoding]
---

# AlgoVeri

Benchmark for generating formally verified code from specifications — not just code that passes tests, but code with machine-checkable correctness proofs.

## Key idea

77 classical algorithms implemented across three verification ecosystems (Dafny, Verus, Lean) with identical functional contracts. This lets you actually compare model performance across paradigms instead of each benchmark testing different tasks.

## Results

- **Dafny:** 40.3% pass rate (Gemini-3 Flash) — SMT automation helps, models can focus on logic
- **Verus:** 24.7% — systems-level memory constraints (ownership, borrowing) trip models up
- **Lean:** 7.8% — explicit proof construction is hard, models struggle badly

## Notable findings

- **Test-time compute matters unevenly:** Gemini-3 effectively uses iterative repair (tripling pass rates in Dafny), while GPT-OSS saturates early — more retries don't help.
- **Language design shapes failure modes:** Dafny lets models focus on logical correctness. Verus and Lean trap models in persistent syntactic and semantic barriers — they can't escape the loop.
- **Verification ≠ testing:** Code that passes all unit tests can still fail verification. The gap between "works on examples" and "provably correct" remains large.

## Why this matters

If agents are going to write production code, especially in correctness-sensitive domains, they need to produce verified code, not just tested code. This benchmark measures how far we are from that. Answer: far, especially beyond Dafny. The Lean result (7.8%) is sobering — explicit proof construction is still mostly beyond current models.

## Repo

https://github.com/haoyuzhao123/algoveri
