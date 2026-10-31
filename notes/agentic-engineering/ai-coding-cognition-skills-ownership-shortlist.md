---
title: "AI coding and the human: cognitive load, skill formation, retention and ownership"
source: "Targeted arXiv search, 2026-10-31"
read_depth: abstract-only
scope_note: "Search shortlist, not five full paper reviews. Code with Me or for Me? read in full separately; the five candidates below were screened through primary abstracts. Selected methods/results/interaction-pattern sections of How AI Impacts Skill Formation were also read. PDFs downloaded for later full reading."
mechanism: "Separate assisted performance, subjective workload, independent learning, delayed retention and ownership before comparing evidence about AI coding."
tags: [developer-cognition, cognitive-load, skill-formation, retention, ownership, human-agent-interaction, research-shortlist]
---

**One-line take:** The closest studies measure reduced acquisition or recall of newly used material and changing developer experience; they do not establish population-wide erosion of developers' existing skills.

## Five close matches, in reading order

### 1. How AI Impacts Skill Formation — Shen and Tamkin

[2601.20245v2](https://arxiv.org/abs/2601.20245v2), January 2026; v2 February 2026. **Best match for learning the skills needed to supervise AI.**

- Randomized study of **52 Python-experienced programmers learning the unfamiliar Trio library**, 26 per condition. AI condition used a GPT-4o chat assistant; both groups took an immediate, unassisted comprehension assessment. The 14-question quiz assessed concepts, code reading and debugging; participants had up to 35 minutes for two coding tasks.
- Main study reports lower comprehension with AI (**Cohen's d = .738, p = .010**), without a statistically significant overall completion-time benefit. It reports a **4.15-point gap on a 27-point quiz**, while describing it as a 17% score difference; 4.15/27 is about 15.4 percentage points. Preserve the raw gap and effect size rather than silently treating those percentages as equivalent.
- Exploratory interaction coding distinguishes wholesale delegation and repeated AI debugging from conceptual inquiry and explanation-seeking. Higher-scoring patterns include generating code then asking follow-up comprehension questions. These are **small observational subgroups**, not randomized evidence that one prompting style causes better learning.
- **Boundary:** immediate skill acquisition, not long-term loss of existing expertise. Any claim that more autonomous agents would worsen learning is extrapolation; this experiment used chat assistance.
- Read depth: abstract plus selected Sections 4.1–4.3, 5.2 and 6. PDF saved; remainder/appendices not fully read. [PDF](../../pdfs/2601.20245v2-skill-formation.pdf) · [text](../../pdfs/2601.20245v2-skill-formation.txt).

### 2. Your Programming Students' Cognition with ChatGPT: Higher Performance, Lower Retention, and Reduced Ownership — Bergh et al.

[2609.21194v1](https://arxiv.org/abs/2609.21194v1), September 2026. **Closest single match across load, recall and ownership.**

- Controlled between-subjects experiment: 59 undergraduate CS students, **55 analyzed**, completing three C tasks with ChatGPT-4.5 or conventional web search. Measures include self-reported effort/difficulty, physiological signals, code attribution and cued recall immediately and **48 hours later**.
- Abstract reports coding scores **89% versus 69%**, but immediate recall **41% versus 53%** and delayed recall **39% versus 52%** for ChatGPT versus control. Students attributed **45% versus 81%** of the submitted code to themselves.
- Crucial qualification: **no significant difference in the amount forgotten over 48 hours**. The evidence is lower recall at both tests, not demonstrated faster forgetting. Lower initial learning/encoding is a possible interpretation, not an isolated causal mechanism.
- Confirmatory physiological trajectories did not differ significantly; substantial signal loss limits interpretation. “Ownership” here is self-attribution of submitted code; do not substitute broad claims about identity, pride or professional alienation.
- Read depth: primary abstract only. [PDF](../../pdfs/2609.21194v1-programming-recall-ownership.pdf) · [text](../../pdfs/2609.21194v1-programming-recall-ownership.txt).

### 3. The Impact of AI Coding Assistants on Software Engineering: A Longitudinal Study — Vella and Blincoe

[2605.23135v1](https://arxiv.org/abs/2605.23135v1), May 2026. **Best match for professional developers' experience over time.**

- Two questionnaires **six months apart**, 158 and 101 eligible respondents; **95 matched** participants. Describes a shift from creating code toward directing, evaluating and correcting AI output: “supervisory engineering work.”
- Abstract reports 84% perceiving better productivity at both times, while the matched cohort reporting worsened experience in at least one dimension rose from **14% to 27%**. Flow and cognitive load worsened while feedback loops improved.
- **Boundary:** longitudinal **self-reported experience**, not randomized AI exposure, measured output productivity or an unassisted skill test. Attrition, self-selection and changing tools/work contexts need full-method review. The 27% figure is not the proportion who lost programming skill.
- Read depth: primary abstract only. [PDF](../../pdfs/2605.23135v1-coding-assistants-longitudinal.pdf) · [text](../../pdfs/2605.23135v1-coding-assistants-longitudinal.txt).

### 4. Beyond Productivity: Measuring Developers' Cognitive Load During GenAI-Supported Software Development — Brandebusemeyer et al.

[2609.37645v1](https://arxiv.org/abs/2609.37645v1), September 2026. **Best match for workload in everyday industrial work.**

- Four-day field study: **21 developers at two SAP sites**, task logs, duration, GenAI use, perceived load and EmbracePlus wristband measurements.
- Abstract finds perceived load associated with both GenAI use and task context, with physiological features adding limited information. It does not give a single direction or effect size in the abstract; do not infer “AI lowers load” from the title.
- **Boundary:** observational associations can reflect which tasks developers choose to use AI for. Wearable measurements are complementary signals, not a direct readout of learning or mental effort.
- Read depth: primary abstract only. [PDF](../../pdfs/2609.37645v1-developer-cognitive-load.pdf) · [text](../../pdfs/2609.37645v1-developer-cognitive-load.txt).

### 5. Beyond the Commit: Developer Perspectives on Productivity with AI Coding Assistants — Chen et al.

[2602.03593v1](https://arxiv.org/abs/2602.03593v1), February 2026. **Best professional-workplace link to ownership and technical expertise.**

- BNY Mellon study: **2,989 developer survey responses and 11 interviews**. Interviews elicit six productivity factors including longer-term technical expertise and ownership of work.
- **Boundary:** perspectives and a measurement framework, not an experiment showing skill decline or loss of ownership. Survey responses are not necessarily 2,989 independent longitudinal participants.
- Read depth: primary abstract only. [PDF](../../pdfs/2602.03593v1-beyond-the-commit.pdf) · [text](../../pdfs/2602.03593v1-beyond-the-commit.txt).

## How these fit the paper already added

[Code with Me or for Me?](code-with-me-or-for-me-developer-workflows.md) directly compares copilot and agent workflows. Its users reported lower load with agents but mixed satisfaction and understanding. That result and the six-month professional survey need not conflict: they compare different tools, populations, exposure histories and measures. Neither alone measures retained skill.

For the original question, keep five outcomes separate:

1. **Assisted performance:** can a person produce a correct artifact while AI is available?
2. **Load/experience:** how effortful, controllable or satisfying does the workflow feel?
3. **Skill formation:** what can the person understand or do independently afterward?
4. **Retention/transfer:** can they still do it after a delay, or in a different problem?
5. **Ownership:** what do they attribute to themselves, and do they feel responsible for it?

A useful next study would assess existing skill before exposure, follow sustained use, then test unassisted retention and transfer. It should randomize interaction design where feasible and measure oversight accuracy alongside task output. The claim that AI causes established expertise to atrophy remains stronger than this screened evidence.

## Search record and lower-priority leads

- Searched the arXiv API on **2026-10-31**, using workload/deskilling/skill-formation terms combined with programming/developer/coding-assistant terms; ownership/pride/identity/frustration combined with AI-assisted programming/coding assistants/vibe coding; and title-based skills/cognition/learning/offloading queries. Screened primary abstracts, not titles alone. This is a targeted discovery pass, **not a systematic literature review**. Snapshot: [query strings, API responses and candidate metadata](../../sources/ai-coding-cognition-arxiv-search-2026-10-31.json).
- [Toward Measuring AI's Effects on Skill Formation: The Stock-Formation Gap](https://arxiv.org/abs/2605.16283v3) — synthesis/research program distinguishing deployed use of existing expertise from formation of future expertise. Useful framing; abstract explicitly rejects claiming proven population-scale erosion.
- [At What Cost? Software Developers' Well-Being in the Age of GenAI](https://arxiv.org/abs/2605.22349v1) — **position paper**, useful for well-being questions rather than causal findings.
- [Towards Decoding Developer Cognition in the Age of AI Assistants](https://arxiv.org/abs/2501.02684v1) — **proposed study** using EEG/eye tracking; the screened abstract reports planned methods, not completed results.
- [The Vibe-Check Protocol](https://arxiv.org/abs/2601.02410v1) — **proposed framework**, not observed skill-decay measurements.
- [It Is Not My Code Anymore](https://arxiv.org/abs/2609.09022v1) — explicitly **no new empirical results**; conceptual authorship/responsibility distinctions. Its title is a closer match than its evidence.

**Sources:** primary arXiv abstracts and archived API responses above; selected main-text sections for Shen/Tamkin. Full PDFs are available locally for follow-up, but downloading a paper is not a full reading.
