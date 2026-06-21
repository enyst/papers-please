# Interpretability — The Circuits Thread

The Anthropic/Olah lineage of mechanistic interpretability work. Four papers that build on each other:

## The progression

1. **Zoom In** (Olah et al., 2020) — Introduction to Circuits. Neural networks contain meaningful features and circuits connecting them. You can understand networks by zooming in and finding interpretable structure.
   - Source: https://distill.pub/2020/circuits/zoom-in/

2. **Toy Models of Superposition** (Elhage et al., 2022) — Why interpretability is hard: networks represent more features than they have neurons by superimposing them. Features are not aligned to individual neurons. Understanding when and how superposition happens.
   - arXiv: https://arxiv.org/abs/2209.10652

3. **Scaling Monosemanticity** (Templeton et al., 2024) — Extracting interpretable features from Claude 3 Sonnet using sparse autoencoders at scale. Found millions of monosemantic features including abstract concepts (Golden Gate Bridge, code errors, deception). Proved the approach works on production-scale models, not just toys.
   - Source: https://transformer-circuits.pub/2024/scaling-monosemanticity/

4. **Attribution Graphs / Circuit Tracing** (Anthropic, 2025) — Tracing how features connect into computational graphs (circuits) inside the model. Open-sourced circuit-tracing tools. Maps the flow from input → features → output for specific behaviors.
   - Source: https://www.anthropic.com/research/open-source-circuit-tracing

## The gap

All of this work is on static models — weights, activations, features in isolation. **None of it has been done on live agents**: agents with tools, memory, multi-turn conversations, environment interaction. The interpretability of an *agent* (why did it choose this tool? why did it remember that? why did it take 12 steps instead of 3?) is a different and unsolved problem.

Understanding a model's features is necessary but not sufficient for understanding an agent's behavior.
