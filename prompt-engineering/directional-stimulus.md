---
name: Directional Stimulus Prompting
description: Guide outputs with subtle hints rather than explicit instructions
category: prompt-engineering
technique: Directional Stimulus Prompting
source: https://arxiv.org/abs/2302.11520
---

```
[WHAT IT IS]
Directional Stimulus Prompting (DSP) uses a small "hint" or stimulus to
guide the model toward a desired output direction without explicitly stating
what the output should be. The hint nudges reasoning without constraining it.
Useful when you want the model to discover an answer but need to steer it
toward the right area.

[BASIC TEMPLATE]
[Task instruction]

Hint: [A directional clue that points toward the right answer or approach]

[HINT TYPES]

--- Keyword hint ---
Summarize this article in 3 bullet points.
Hint: Focus on economic impact.

--- Directional hint ---
What is causing this bug in my code?
Hint: Consider the order in which variables are initialized.

--- Perspective hint ---
Write a review of this product.
Hint: Consider the experience of a first-time user who is not tech-savvy.

--- Constraint hint ---
Solve this math problem.
Hint: Consider whether there might be a solution that doesn't require algebra.

--- Quality hint ---
Write a subject line for this email.
Hint: The reader should be curious, not obligated.

[EXAMPLE — Summary with directional hint]
Without hint:
Input: [Long article about a new electric vehicle]
Output: "Company X releases new EV. It has 400-mile range. Pre-orders open now."

With hint "Hint: Focus on what makes this different from competitors":
Output: "Unlike rivals, Company X's EV charges to 80% in 12 minutes using standard outlets — no special infrastructure required."

[EXAMPLE — Code review with directional hint]
Without hint:
"Review this function."
→ Generic review covering style, logic, etc.

With hint "Hint: Consider what happens when the input list is empty":
→ Immediately focuses on edge case handling

[GENERATING HINTS AUTOMATICALLY]
If you're using DSP at scale, you can generate hints programmatically:

PROMPT: Given this task and input, generate a helpful hint that would
guide an AI toward the most important aspect to focus on.
Do not give the answer — only a directional nudge.

Task: [task description]
Input: [sample input]

Hint:

[NOTES]
- Hints work best when the model has the capability to produce the right output
  but needs steering — they don't add new knowledge.
- Too specific a hint becomes an instruction; too vague, it adds no value.
  The sweet spot is a hint that opens a door without walking through it.
- Hints are particularly useful in multi-turn systems where you want to subtly
  adjust behavior without rewriting the system prompt.
- Combine with few-shot: provide examples + a hint for maximum steering power.
- DSP showed significant improvements on summarization and dialogue tasks in
  the original paper (Microsoft Research, 2023).
```
