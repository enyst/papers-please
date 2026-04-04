---
title: "Evaluating Memory Structure in LLM Agents"
authors:
  - Alina Shutova
  - Alexandra Olenina
  - Ivan Vinogradov
  - Anton Sinitsin
arxiv_id: "2602.11243"
arxiv_url: "https://arxiv.org/abs/2602.11243"
published: "2026-02-11"
updated: "2026-02-11"
source: "arXiv"
project: "memory"
scope_note: "pass-two meta include: benchmark"
agent_setting: "LLM agents and assistants with structured long-term memory"
memory_mechanism: "Benchmark paper that tests whether agents can organize memory into useful structures like ledgers, lists, and trees, not just recall isolated facts."
icl_relevance: "medium"
tags:
  - agent-memory
  - benchmark
  - memory-structure
  - evaluation
categories:
  - cs.LG
  - cs.CL
---

- **One-line take:** Argues that memory quality is partly about structure, not just retrieval score on stored facts.
- **What it stores:** The benchmark probes systems that explicitly maintain structured memory objects instead of loose snippets.
- **How memory is used at inference time:** Benchmark paper that tests whether agents can organize memory into useful structures like ledgers, lists, and trees, not just recall isolated facts.
- **Why it matters for this sub-project:** A strong complement to the mechanism papers because it clarifies how to evaluate whether fancy memory structures are actually being used well.
- **Caveats / limits:** The benchmark is diagnostic and narrow by design, so it does not replace broader long-horizon task evaluations.
- **Abstract-level summary:** Modern LLM-based agents and chat assistants rely on long-term memory frameworks to store reusable knowledge, recall user preferences, and augment reasoning. As researchers create more complex memory architectures, it becomes increasingly difficult to analyze their capabilities and guide future memory designs. Most long-term memory benchmarks focus on simple fact retention, multi-hop recall, and time-based changes. While undoubtedly important, these capabilities can often be achieved with simple retrieval-augmented LLMs and do not test complex memory hierarchies. To bridge this gap, we propose StructMemEval - a benchmark that tests the agent's ability to organize its long-term memory, not just factual recall. We gather a suite of tasks that humans solve by organizing their knowledge in a specific structure: transaction ledgers, to-do lists, trees and others. Our initial experiments show that simple retrieval-augmented LLMs struggle with these tasks, whereas memory agents can reliably solve them if prompted how to organize their memory. However, we also find that modern LLMs do not always recognize the memory structure when not prompted to do so. This highlights an important direction for future improvements in both LLM training and memory frameworks.
