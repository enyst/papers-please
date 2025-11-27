Recommended by N:
- Hayati et al, 2018 - Retrieval-Based Neural Code Generation
- Zhou et al, 2022 - RAG for LLMs


- MemoRAG: Moving towards Next-Gen RAG Via Memory-Inspired Knowledge Discovery
	- https://arxiv.org/abs/2409.05591
- Retrieval Augmented Generation or Long-Context LLMs? A Comprehensive Study and Hybrid Approach
	- https://arxiv.org/abs/2407.16833
	- Results reveal that when resourced sufficiently, LC consistently outperforms RAG in terms of average performance. However, RAG's significantly lower cost remains a distinct advantage. Based on this observation, we propose Self-Route, a method that routes queries to RAG or LC based on model self-reflection.
- Memory 3: Language Modeling with Explicit Memory
	- https://x.com/rohanpaul_ai/status/1825729380544377009?s=61
	- https://arxiv.org/abs/2407.01178

Astute RAG: Overcoming Imperfect Retrieval Augmentation and Knowledge Conflicts for Large Language Models
https://arxiv.org/pdf/2410.07176

CONTEXTUAL DOCUMENT EMBEDDINGS
https://arxiv.org/pdf/2410.02525
https://notebooklm.google.com/notebook/be5ded78-7fc3-4df4-b88e-3488cf50d994?authuser=1

AGENT WORKFLOW MEMORY
https://arxiv.org/pdf/2409.07429

SCIENCEAGENTBENCH:  TOWARD RIGOROUS ASSESSMENT OF LANGUAGE AGENTS FOR DATA-DRIVEN SCIENTIFIC DISCOVERY
https://arxiv.org/pdf/2410.05080
	- paper mentioning OpenHands?

(and the other is MLEBench)



Prompt Engineering:
- Chain of Thought
- Self-consistency
- Generated Knowledge

When GPT-4 receives an input prompt, the input text will be firstly converted into tokens that the model can interpret and process. These tokens are then managed by transformer layers, which capture their relationships and context. Within these layers, attention mechanisms distribute different weights to tokens based on their relevance and context. After attention processing, the model forms its internal renditions of the input data, known as intermediate representations. These representations are then decoded back into human-readable text [[38](https://arxiv.org/html/2310.14735v3#bib.bib38)].

A significant aspect of this process is the randomness function [[39](https://arxiv.org/html/2310.14735v3#bib.bib39)]. This function is influenced by two primary parameters, temperature and top-k sampling. The first one, temperature [[40](https://arxiv.org/html/2310.14735v3#bib.bib40)] balances the randomness and determinism in the output. A higher temperature value results in more random outputs, while a lower value makes the output more deterministic. The second one, top-ksampling [[41](https://arxiv.org/html/2310.14735v3#bib.bib41)], limits the model’s choices to the top k most probable tokens during each step of output generation. The final stage of this process is the output generation, where the model crafts the final text.


------- o1 like PROMPTING ---------
--- Prompt-based

0) CoT et al: arxiv.org/pdf/2201.11903

It started with Chain-of-Thought paper. This class of methods boils down to asking the LLM nicely to reveal its internal thoughts (e.g. "Let's think step by step"; more generally telling the model to disclose the intermediate computation steps in someway).

A simple variation on CoT would be "CoT self-consistency" -> i.e. sample multiple CoT traces in parallel and use majority voting to find the "right" answer.

1) ToT (tree of thought): arxiv.org/pdf/2305.10601

Further complexifies the above (in CS terms we go from linear list -> tree): build up an m-ary tree of intermediate thoughts (thoughts = intermediate steps of CoT); at each thought/node:

a) run the “propose next thoughts” prompt (or just sample completions m times)
b) evaluate those thoughts (either independently or jointly)
c) keep the top m

cons: very expensive & slow
pro: works with off-the-shelf LLMs

2) Self-Reflection: arxiv.org/pdf/2405.06682

If incorrect response pass the self-reflection feedback back to an LLM before attempting to re-answer again; 

As an input self-reflection gets a gold answer and is prompted to explain how it would now solve the problem. The results are redacted before passing back the feedback to avoid leaking the solution. 

Even re-answering given only a binary feedback (“your previous answer was incorrect”) is significantly stronger than the baseline (no feedback, just sample a response once).

3) Self-Contrast: arxiv.org/pdf/2401.02009

a) create multiple solutions by evaluating diverse prompts derived from the original question (yields diverse perspectives on how to solve the problem
b) pairwise contrast the solutions
c) generate a todo checklist in order to revise the generations from a)

4) Think Before You Speak: arxiv.org/pdf/2311.07445

Introduces the CSIM method: 5 prompts that make the model better at dialogue applications.

5 prompts they use to help improve the communication skills are "empathy", "topic transition", "proactively asking questions", "concept guidance", "summarizing often".

Their LLM has 2 roles: thinking and speaking. The thinking role, or the “inner monologue” is occasionally triggered by the 5 prompts and is not displayed to the user but is instead used as the input for the user-facing speaking role.



---

