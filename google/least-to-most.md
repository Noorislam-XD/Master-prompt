---
name: Least-to-Most Prompting
description: Decompose hard problems into easier sub-problems and solve sequentially
category: google
technique: Least-to-Most Prompting
source: https://arxiv.org/abs/2205.10625
---

```
[WHAT IT IS]
Least-to-most prompting decomposes a complex problem into a sequence of
simpler sub-problems, where each sub-problem builds on the previous solution.
Developed by Google Research. Outperforms standard chain-of-thought on
tasks requiring systematic decomposition (math, multi-step reasoning).

[TWO-PHASE TEMPLATE]

PHASE 1 — Decompose:
Break the following problem into a sequence of simpler sub-problems that
must be solved in order. List them from easiest to hardest.

Problem: [complex problem]

Sub-problems:
1. [easiest sub-problem]
2. [next sub-problem — may use answer from #1]
3. [next — may use answers from #1 and #2]
...

PHASE 2 — Solve sequentially:
Now solve each sub-problem in order, using previous answers:

Sub-problem 1: [restate it]
Solution: [solve it]

Sub-problem 2: [restate it, incorporating answer from #1]
Solution: [solve it]

...

Final answer: [combine all sub-solutions]

[SINGLE PROMPT VERSION]
To solve this problem, first identify the simpler sub-questions I need to
answer, starting from the easiest. Then answer each one in order, using
earlier answers to help with later ones.

Problem: [your problem here]

[EXAMPLE]
Problem: "A store has 3 types of gift boxes: small ($5), medium ($8), and large ($12).
A customer buys 4 small, 2 medium, and 1 large. They have a 10% discount coupon.
Tax is 8%. What is the final price?"

Decomposition:
1. What is the cost of the small boxes?
2. What is the cost of the medium boxes?
3. What is the cost of the large boxes?
4. What is the subtotal?
5. What is the price after the 10% discount?
6. What is the final price after 8% tax?

Solutions:
1. 4 × $5 = $20
2. 2 × $8 = $16
3. 1 × $12 = $12
4. $20 + $16 + $12 = $48
5. $48 × 0.90 = $43.20
6. $43.20 × 1.08 = $46.66

Final answer: $46.66

[BEST USE CASES]
- Multi-step math word problems
- Programming tasks with interdependent components
- Research questions that require building up context
- Planning tasks where earlier decisions constrain later ones

[NOTES]
- The decomposition step is the most important — bad decomposition leads to bad answers.
- Works best when sub-problems have clear, reusable outputs.
- Combine Phase 1 and Phase 2 in one prompt for simpler problems; separate them for complex ones.
- Showed large gains on symbolic manipulation and math tasks in the original Google Research paper.
```
