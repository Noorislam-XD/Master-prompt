---
name: Extended Thinking
description: Give Claude dedicated thinking time before responding for hard problems
category: anthropic
technique: Extended Thinking
source: https://docs.anthropic.com/en/docs/build-with-claude/extended-thinking
---

```
[WHAT IT IS]
Extended thinking gives Claude a scratchpad to reason through complex problems
before producing its final response. The thinking block is streamed separately
and is not part of the assistant's visible output — it's Claude "showing its work."

Available on: Claude 3.7 Sonnet and later models via the Anthropic API.

[API USAGE]
import anthropic

client = anthropic.Anthropic()

response = client.messages.create(
    model="claude-3-7-sonnet-20250219",
    max_tokens=16000,
    thinking={
        "type": "enabled",
        "budget_tokens": 10000  # How many tokens Claude can use for thinking
    },
    messages=[{
        "role": "user",
        "content": "YOUR HARD QUESTION HERE"
    }]
)

# Separate thinking from response
for block in response.content:
    if block.type == "thinking":
        print("THINKING:", block.thinking)
    elif block.type == "text":
        print("RESPONSE:", block.text)

[SYSTEM PROMPT — Instruct for deliberate reasoning]
Before answering, think carefully through this problem. Consider multiple
approaches, check your assumptions, and verify your reasoning before committing
to a final answer. Hard problems deserve careful thought.

[PROMPT TEMPLATE — Hard reasoning task]
<problem>
[Describe the complex problem here]
</problem>

Think through this step by step. Show all assumptions you are making.
If there are multiple valid approaches, reason through the trade-offs
before recommending one. Give your final answer only after completing
your analysis.

[BEST USE CASES]
- Complex math and logic problems
- Multi-step planning with many constraints
- Code architecture decisions with significant trade-offs
- Legal or medical reasoning that requires considering many factors
- Any task where you've found standard prompting produces shallow or wrong answers

[NOTES]
- budget_tokens controls how much thinking Claude does: 1,000–3,000 for moderate tasks, 10,000+ for very hard problems.
- Extended thinking increases latency and cost — use only when the extra reasoning meaningfully improves accuracy.
- Thinking tokens are billed at the same rate as output tokens.
- Do NOT summarize or paraphrase the thinking block in your final prompt — let Claude reason freely.
- Streaming is recommended for extended thinking to show progress to users.
- You cannot access thinking blocks in subsequent turns (they are not returned in context).
```
