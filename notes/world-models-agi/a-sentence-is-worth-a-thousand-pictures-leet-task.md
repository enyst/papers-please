---
title: "A sentence is worth a thousand pictures: can large language models understand hum4n L4ngu4ge and the W0rld behind W0rds?"
authors:
  - (see paper)
  - Gary Marcus
  - Fritz Günther
  - Elliot Murphy
doi: "10.1098/rsta.2025.0008"
url: "https://royalsocietypublishing.org/doi/full/10.1098/rsta.2025.0008"
published: "2026-05-14"
source: "Phil. Trans. R. Soc. A 384(2320) — theme issue 'World models in natural and artificial intelligence'"
article_type: "Research article"
read_depth: "full"
mechanism: "Introduces a 'leet task' (l33t: letters systematically replaced by numbers) to test whether LLMs use top-down, grounded, world-experience feedback or only fixed word↔vector associations. Humans excel; models struggle."
tags:
  - grounding
  - top-down-processing
  - concept-formation
  - language-understanding
  - llm-limits
  - neurosymbolic
categories:
  - artificial intelligence
---

- **One-line take:** A neat, falsifiable probe of grounding: humans decode `l33t`/`W0rd` text easily because top-down expectations from world experience flow down and reshape perception; LLMs — leaning on fixed token↔vector associations without grounded cognition — struggle. Evidence that scaling alone doesn't buy human-like understanding.

- **The two-part argument:**
  1. **Tool vs theory:** distinguishes using LLMs as *atheoretical mechanistic tools* (useful) from treating them as *theoretically informative representations* of the human language system (unearned). A good tool is not a good theory of the target system.
  2. **Top-down feedback needs grounding:** human comprehension uses feedback from higher levels (expectations, past world experience) to disambiguate/repair degraded input. Their hypothesis: lacking grounded cognition, models can't exploit this and fall back on fixed associations.

- **The experiment (l33t t4sk):** decode sentences where letters are systematically swapped for numerals. Requires holding a hypothesis about meaning and pushing it back down onto the noisy surface. Humans excel; models struggle — the predicted signature of missing top-down grounded repair.

- **Their reading of the gap:** what's missing isn't captured by more scale — it's domain-specific operations and *non-linguistic world models*. Human language works by interfacing with non-linguistic reasoning/perception systems; models shouldn't be deprived of that. Points to neurosymbolic combinations (deep learning + symbolic cognition) as the path. Cites Mitchell & Krakauer: understanding a tickle maps a word to a *sensation*, not to another word.

- **Caveats / stance:** the authors (incl. Gary Marcus) are on the skeptical side of the "LLMs understand" debate, so read the framing as a strong prior; but the leet task is a concrete, reproducible behavioural dissociation, not just polemic.

- **Why it matters for us:** grounding + top-down repair is the crux of the concept-formation question Engel cares about. For agents it also predicts a real failure mode: robust performance on in-distribution surface forms, brittle collapse when the surface is perturbed in ways a grounded understander would sail through.

- **Abstract:** LLMs are linked to claims of human-like linguistic performance and hailed as steps toward AGI and as models of human language. The authors analyse LLMs as theoretically informative representations vs atheoretical tools, and evaluate their ability to use top-down feedback (which requires grounding in expectations and world experience). Hypothesizing that models lack grounded cognition and rely on fixed word↔vector associations, they run a novel leet task (decoding letter→number sentences); humans excel, models struggle. They identify key missing abilities that scaling alone won't solve.
