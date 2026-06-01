---
name: Zero-Shot Chain-of-Thought
description: Trigger step-by-step reasoning with a single phrase — no examples needed
category: google
technique: Zero-Shot CoT
source: https://arxiv.org/abs/2205.11916
---

```
[WHAT IT IS]
Adding "Let's think step by step" (or variants) to a prompt triggers
chain-of-thought reasoning without providing any examples. Discovered by
Kojima et al. (2022) and validated across many models including Google's PaLM.
Simple, free, and effective for reasoning tasks.

[TRIGGER PHRASES — by task type]

General reasoning:
"Let's think step by step."

Math:
"Let's work through this carefully, one step at a time."

Logic:
"Let's reason through this systematically."

Decision-making:
"Let's think through the pros and cons before deciding."

Debugging:
"Let's trace through what's happening step by step."

Planning:
"Let's break this down into steps before starting."

[TEMPLATES]

--- Basic ---
[Your question or problem here]

Let's think step by step.

--- With format instruction ---
[Your question or problem here]

Think through this step by step, then give your final answer on a new line
starting with "Answer:".

--- Two-stage (more reliable) ---
Stage 1 prompt:
[Question]. Let's think step by step.

→ Model produces reasoning

Stage 2 prompt:
Therefore, the answer is:

→ Model commits to final answer

[EXAMPLE]
Problem: "Roger has 5 tennis balls. He buys 2 more cans of tennis balls.
Each can has 3 balls. How many tennis balls does he have now?"

Without CoT trigger: "11" (often wrong without reasoning)

With "Let's think step by step":
"Roger starts with 5 tennis balls.
He buys 2 cans × 3 balls = 6 more balls.
Total: 5 + 6 = 11 tennis balls.
Answer: 11" ✓

[NOTES]
- Works best on tasks with a verifiable correct answer: math, logic, science.
- For simple factual questions, CoT adds no value and wastes tokens.
- "Let's think step by step" outperforms many more elaborate CoT prompts on benchmarks.
- Combine with self-consistency (multiple samples + majority vote) for maximum accuracy.
- For production, use the two-stage version to reliably separate reasoning from the final answer.
- Temperature: use 0 for deterministic answers, 0.5–0.7 for self-consistency sampling.
```
