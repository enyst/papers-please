---
title: "Minds, Brains, and Programs (the Chinese Room Argument)"
authors:
  - John R. Searle
doi: "10.1017/S0140525X00005756"
url: "https://www.cambridge.org/core/journals/behavioral-and-brain-sciences/article/minds-brains-and-programs/DC644B47A4299C637C89772834C7060F"
published: "1980"
source: "Behavioral and Brain Sciences, Vol. 3, No. 3 (1980), pp. 417–457 (with open peer commentary)"
article_type: "Classic philosophy paper"
read_depth: "classic (from knowledge)"
mechanism: "Thought experiment: a person who knows no Chinese, following an English rulebook to manipulate Chinese symbols, can pass a Chinese Turing test while understanding nothing — so running the right program (syntax) is not sufficient for understanding/meaning (semantics)."
tags:
  - understanding
  - symbol-grounding
  - syntax-vs-semantics
  - intentionality
  - strong-ai
  - turing-test
  - chinese-room
  - classic
categories:
  - artificial intelligence
---

- **One-line take:** The canonical argument against "**Strong AI**" (that a suitably programmed computer *has a mind* and *understands*). A person in a room, with no Chinese, mechanically applies a rulebook to map Chinese input symbols to Chinese output symbols, convincingly passing for a Chinese speaker — yet understands not a word. Moral: **syntax (symbol manipulation) is not sufficient for semantics (meaning/understanding)**, so passing the behavioural test ≠ understanding.

- **The setup:** Searle imagines himself as the CPU. Inputs (Chinese questions) come in; he looks up formal rules ("if you see these squiggles, write those squiggles"); outputs (Chinese answers) go out, indistinguishable from a native speaker's. He does everything the program does. He still has zero understanding of Chinese. Since he *is* the whole computational process, running the program can't be what constitutes understanding.

- **Target — the distinction that matters:** "**Strong AI**" (the program literally understands / has cognitive states) vs "**Weak AI**" (the computer is a powerful tool for studying the mind). Searle only attacks Strong AI. The deep claim: **programs are formal/syntactic; minds have semantic content (intentionality — aboutness)**; and you can't get semantics from syntax alone.

- **The famous replies + Searle's answers** (this is why the paper endures — it's a whole dialectic):
  - **Systems reply:** "the *room as a whole* understands, even if the person doesn't." Searle: let the person **memorize the rulebook** and work outdoors — now there's no system but him, and he still understands nothing.
  - **Robot reply:** "put the program in a robot with sensors/actuators — grounding fixes it." Searle: replace the robot's brain with the room; adding transducers adds more symbols, not meaning. (Note: many find this the *weakest* rebuttal — it's essentially the symbol-grounding objection, and it's where a lot of modern embodiment/grounding work pushes back.)
  - **Brain-simulator reply:** "simulate the actual neuron firings of a Chinese speaker." Searle (water-pipes variant): simulating the *form* of neural activity still simulates only structure, not causal powers.
  - **Combination / other-minds / etc.** — each answered in kind.

- **The positive thesis (easy to miss):** Searle is a biological naturalist, **not** a dualist. He thinks machines can think — *we* are such machines (biological ones). His claim is that understanding depends on the specific **causal powers** of the brain's biology, which a mere formal program (implementable on anything) does not thereby possess. "Could a machine think? Yes — the brain is one. Could a digital computer think *in virtue of running a program*? No."

- **Why it's foundational to this issue:** this is the direct ancestor of the RSTA issue's grounding/understanding papers — the **l33t-task** paper ("fixed word↔vector associations, no grounded cognition") is essentially an empirical Chinese-Room probe, and **"Is there an 'I' in AI?"** inverts Searle ("when words act like things, they *do* mean them"). The symbol-grounding problem (Harnad, 1990) is the formalization of the Robot-reply debate this paper started. Whenever someone says "the LLM only does statistics, it doesn't *understand*," they are, knowingly or not, running the Chinese Room.

- **Why it matters for us:** the permanent caution against inferring understanding from fluent output. It sharpens the practical question for agents: if syntax isn't sufficient for semantics, then what *would* count as an agent understanding its task rather than pattern-matching it? The modern candidates — grounding, causal world models, empowerment, top-down repair (all in this issue) — are attempts to add the thing the pure rulebook lacks. Also worth the honest counterweight: many working researchers reject Searle's conclusion (the Systems and Robot replies never died), so treat it as the enduring *statement of the problem*, not a closed case.

- **Famous line:** "The computer... has a syntax but no semantics."
