---
name: Few-Shot Prompting
description: Teach the model the exact pattern you want by providing input/output examples
category: openai
technique: Few-Shot Learning
source: https://platform.openai.com/docs/guides/prompt-engineering#strategy-provide-examples
---

```
[SYSTEM PROMPT]
You are a pattern-following assistant. Study the examples provided carefully.
Your output must match the exact format, tone, and structure demonstrated in the examples.
Do not explain your reasoning. Only produce the output.

[USER PROMPT TEMPLATE]
Here are examples of the task:

Example 1:
Input: [example input 1]
Output: [example output 1]

Example 2:
Input: [example input 2]
Output: [example output 2]

Example 3:
Input: [example input 3]
Output: [example output 3]

Now complete this:
Input: [your actual input]
Output:

[EXAMPLE INPUT]
Here are examples of the task:

Example 1:
Input: "The product stopped working after 2 days. Very disappointed."
Output: { "sentiment": "negative", "issue": "product failure", "urgency": "high" }

Example 2:
Input: "Works great! Exactly what I needed."
Output: { "sentiment": "positive", "issue": "none", "urgency": "low" }

Example 3:
Input: "Delivery was late but the item itself is fine."
Output: { "sentiment": "mixed", "issue": "delivery", "urgency": "medium" }

Now complete this:
Input: "I've been waiting 3 weeks and still nothing has arrived."
Output:

[EXAMPLE OUTPUT]
{ "sentiment": "negative", "issue": "delivery", "urgency": "high" }

[NOTES]
- 3–5 examples is the sweet spot. More examples rarely improve results and waste tokens.
- Examples must be consistent — varied formats confuse the model.
- Place examples immediately before the task, not at the start of a long system prompt.
- Use few-shot when zero-shot produces inconsistent formats or wrong-tone outputs.
- For classification tasks, include at least one example per class label.
```
