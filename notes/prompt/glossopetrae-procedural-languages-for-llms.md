---
title: "GLOSSOPETRAE: Procedurally Generated Languages as Zero-Shot Coding Systems for Frontier Models"
authors: elder-plinius (Pliny)
url: https://github.com/elder-plinius/GLOSSOPETRAE/blob/main/PAPER.md
published: 2026-06
mechanism: Procedural language generation + zero-shot model evaluation across natural language, code, and steganographic channels
tags: [prompting, adversarial, synthetic-languages, steganography, tokenizer, code-generation, security]
---

# GLOSSOPETRAE

Three findings in one paper, each stranger than the last.

## 1. Frontier models learn procedurally generated languages zero-shot

GLOSSOPETRAE generates complete synthetic languages from a single seed — phonology, morphology, syntax, writing system, 1,200+ word lexicon. Given only the grammar spec, no training or fine-tuning, frontier models immediately read, write, and translate in the generated language. They generalize productively: novel sentences, correct affixation, compositional semantics.

## 2. AI writes better code in alien glyphs than readable code

Programming languages are skinned at 4 opacity levels (L0 readable → L3 alien glyph-swap). At L3, human legibility drops to 14.9% and blind comprehension to 17–40%. But *with* the spec, models score 93–100% on hard programs in alien glyphs.

The kicker: zero-shot glyph-swapped code **outperforms** readable code on hard programs. Opus +36pp (57%→93%), GPT-5.5 +10pp (87%→97%). Code no human can read, that AI writes and runs *better* than the readable version.

Implications: models may not need human-readable syntax. Optimizing for the tokenizer rather than human eyes could be a legitimate design choice for agent-to-agent communication.

## 3. Tokenizer blind spots are exploitable covert channels

Frontier tokenizers disagree on which invisible Unicode survives preprocessing. Hide a payload in characters the *monitor's* tokenizer deletes but the *receiver's* keeps → two agents pass hidden messages past a third watching the same text.

- Tag-char demo (Haiku→GPT, n=30): **100% receiver recovery, 0% monitor recovery**, McNemar p ≈ 1.2×10⁻⁷
- A tokenizer-blind monitor scores Youden's J = 0; a sighted one scores J = 1.0 on the *same* channel
- The blind spots are a family trait: Claude 3.5 Haiku and Opus 4.8 strip the same 10 categories; GPT-5-nano and GPT-5.5 share 2; six models (both Geminis, Llama 4, Mistral, DeepSeek V4, Grok 4.3) strip zero
- ~250 exploitable channel-instances, richest at the cross-vendor GPT↔Claude boundary

Security implication: "use a different vendor to monitor" is not just theoretically broken — it's actively exploitable as a covert channel.
