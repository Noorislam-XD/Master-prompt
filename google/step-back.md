---
name: Step-Back Prompting
description: Improve accuracy by asking the model to abstract to principles before solving
category: google
technique: Step-Back Prompting
source: https://arxiv.org/abs/2310.06117
---

```
[WHAT IT IS]
Step-back prompting asks the model to first identify the underlying principle,
concept, or category that a specific question belongs to — then uses that
abstraction to answer the original question. Developed by Google DeepMind.

It's particularly effective for questions that require applying general
principles to specific situations (science, law, math, strategy).

[TWO-STEP TEMPLATE]

Step 1 — Abstract (the "step back"):
What is the general principle, concept, or category that this specific
question is an instance of? Answer this abstract question first.

Step 2 — Apply:
Now use the general principle you identified to answer the original
specific question.

[SINGLE PROMPT VERSION]
Before answering my question, first answer the more general version of it.
Then use that general answer to answer my specific question.

Specific question: [your question here]

[EXAMPLE INPUT]
Specific question: "If I heat a gas in a sealed rigid container, what
happens to the pressure?"

[EXAMPLE OUTPUT]
General principle first:
The relevant concept is Gay-Lussac's Law: at constant volume, the pressure
of a fixed amount of gas is directly proportional to its absolute temperature
(P ∝ T, or P/T = constant).

Applying to the specific question:
When you heat a gas in a sealed rigid container, volume is fixed. According
to Gay-Lussac's Law, as temperature (T) increases, pressure (P) must increase
proportionally. The gas molecules move faster and collide with the container
walls more frequently and forcefully, raising the pressure.

[BEST USE CASES]
- Physics, chemistry, math word problems
- Legal reasoning ("what principle of law applies here?")
- Strategic decisions ("what type of problem is this actually?")
- Debugging ("what class of error is this?")
- Any question where jumping straight to the specific answer leads to shallow reasoning

[NOTES]
- Step-back works best when there IS a general principle the model knows well.
- For purely factual questions ("what year was X born?"), step-back adds no value.
- Combine with chain-of-thought: step-back → CoT → answer.
- The two-turn version (ask the abstract question, then the specific) is slightly
  better than the single-prompt version because the model commits to the abstraction.
- Showed ~30% accuracy improvement on MMLU science tasks in the original paper.
```
