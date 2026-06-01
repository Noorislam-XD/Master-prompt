---
name: Self-Consistency
description: Generate multiple independent answers and take the majority vote for accuracy
category: google
technique: Self-Consistency
source: https://arxiv.org/abs/2203.11171
---

```
[WHAT IT IS]
Self-consistency samples multiple reasoning paths from the model (using a
higher temperature) and returns the most common final answer. It is the
ensemble method for LLMs — more reliable than a single chain-of-thought pass.
Developed at Google Brain.

[SINGLE PROMPT VERSION]
Solve this problem 3 different ways, using a different approach each time.
Then identify which answer appears in the majority of your solutions.

Problem: [your problem here]

Solution 1:
[reasoning path 1]

Solution 2:
[reasoning path 2]

Solution 3:
[reasoning path 3]

Majority answer: [the answer that appears most often]

[API VERSION — programmatic]
import anthropic

client = anthropic.Anthropic()
QUESTION = "A train travels 120km in 1.5 hours. What is its average speed?"

answers = []
for i in range(5):  # Generate 5 independent answers
    response = client.messages.create(
        model="claude-opus-4-5",
        max_tokens=500,
        temperature=0.7,  # Higher temp = more diverse paths
        messages=[{
            "role": "user",
            "content": f"Solve step by step: {QUESTION}\nFinal answer (number only):"
        }]
    )
    answers.append(response.content[0].text.strip())

from collections import Counter
majority = Counter(answers).most_common(1)[0][0]
print(f"Majority answer: {majority}")
print(f"All answers: {answers}")

[EXAMPLE]
Problem: "A bat and ball cost $1.10 total. The bat costs $1.00 more than the ball. How much does the ball cost?"

Path 1: Let ball = x. Bat = x + 1.00. Total: 2x + 1.00 = 1.10 → x = 0.05. Ball costs $0.05. ✓
Path 2: If ball = $0.10, bat = $1.10, total = $1.20. Too much. Try $0.05: bat = $1.05, total = $1.10. ✓
Path 3: Algebra: x + (x+1) = 1.10 → 2x = 0.10 → x = 0.05. Ball = $0.05. ✓

Majority answer: $0.05

[BEST USE CASES]
- Math problems where a single chain-of-thought might make arithmetic errors
- Logic puzzles with a definitive right answer
- Multiple-choice questions where you want higher confidence
- Any task where you can score or compare outputs

[NOTES]
- Use temperature 0.5–0.8 for diverse but not incoherent paths.
- 5–10 samples gives reliable majority voting; 3 is minimum.
- Cost scales linearly — 5 samples = 5x cost. Use for high-stakes questions only.
- Self-consistency only helps when there IS a single correct answer.
  It does not improve creative or subjective tasks.
- Combine with step-back for maximum accuracy on hard reasoning.
```
