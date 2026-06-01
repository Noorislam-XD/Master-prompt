---
name: Tree of Thoughts (ToT)
description: Explore multiple reasoning paths simultaneously for complex decisions
category: prompt-engineering
technique: Tree of Thoughts
source: https://arxiv.org/abs/2305.10601
---

```
[WHAT IT IS]
Tree of Thoughts extends chain-of-thought by exploring multiple reasoning
branches simultaneously and evaluating each. The model acts as both problem
solver (generating branches) and evaluator (scoring them). Developed at
Princeton and Google. Best for problems where the optimal path is unclear.

[SIMPLIFIED SINGLE-PROMPT VERSION]
Imagine three different experts are solving this problem.
Each expert writes out their first step, then all experts share their step.
Any expert who realizes their step was wrong drops out.
The experts continue until one reaches the final answer.

Problem: [your problem here]

[STRUCTURED VERSION — 3 branches]
I will explore 3 different approaches to this problem, evaluate each,
and select the best one to complete.

Problem: [your problem here]

BRANCH 1 — [Approach name]:
Step 1: [first reasoning step]
Step 2: [second step]
Evaluation: [Is this working? Is this a dead end? Confidence: high/medium/low]

BRANCH 2 — [Different approach]:
Step 1: [first reasoning step]
Step 2: [second step]
Evaluation: [Is this working? Confidence: high/medium/low]

BRANCH 3 — [Another approach]:
Step 1: [first reasoning step]
Step 2: [second step]
Evaluation: [Is this working? Confidence: high/medium/low]

SELECTION: Branch [N] is most promising because [reason].

COMPLETING BRANCH [N]:
[Continue the best branch to completion]

FINAL ANSWER: [result]

[EXAMPLE]
Problem: "What is the best way to cross a river without a bridge, given
you have a rope, a log, and 3 people?"

Branch 1 — Raft approach:
Step 1: Lash the log horizontally to create a platform...
Evaluation: The log alone is unstable. Medium confidence.

Branch 2 — Rope bridge approach:
Step 1: Tie rope to tree on one bank, swim rope to other side...
Evaluation: Requires swimming which is risky. Low confidence.

Branch 3 — Guided float approach:
Step 1: One person swims with rope. Others hold the rope as guide...
Evaluation: Safest use of all resources. High confidence.

Selection: Branch 3. Completing...
Final Answer: [detailed plan using Branch 3]

[BEST USE CASES]
- Creative problems with multiple valid solutions
- Strategic planning decisions
- Puzzle solving and game playing
- Any problem where you suspect your first instinct might be wrong

[NOTES]
- ToT is expensive — use only when the problem genuinely has multiple plausible paths.
- The "3 experts" single-prompt version is much simpler and often sufficient.
- For programmatic use: generate N candidates at temperature 0.7, score each,
  expand the top K, repeat. This is BFS/DFS over reasoning states.
- Works best with more capable models (GPT-4 class and above).
- LangChain and LlamaIndex have experimental ToT implementations.
```
