---
name: Prompt Chaining
description: Break complex tasks into sequential sub-prompts, passing outputs forward
category: anthropic
technique: Prompt Chaining
source: https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/chain-prompts
---

```
[WHAT IT IS]
Prompt chaining breaks a complex task into a sequence of focused sub-tasks.
Each prompt does one thing well, and its output becomes the input for the next.
This is more reliable than a single mega-prompt trying to do everything at once.

[WHEN TO USE]
- The task has clear sequential stages (research → plan → write → review)
- Any single stage is complex enough to deserve its own focused prompt
- You need a human checkpoint between stages
- Earlier stages produce structured data that later stages need

[CHAIN TEMPLATE]

--- STEP 1: Extract / Research ---
System: You are a [role]. Extract the following from the provided text.
Return ONLY a JSON object. No explanation.

Schema: { "key1": ..., "key2": ..., "key3": ... }

User: <text>[input text]</text>

→ Output: { JSON object }

--- STEP 2: Plan (uses Step 1 output) ---
System: You are a [role]. You will receive structured data and must produce
a detailed plan. Return your plan as a numbered list.

User: <data>[paste Step 1 JSON output here]</data>

Based on this data, create a step-by-step implementation plan.

→ Output: [numbered plan]

--- STEP 3: Execute (uses Step 2 output) ---
System: You are a [role]. Follow the provided plan exactly.

User: <plan>[paste Step 2 plan here]</plan>

Execute this plan and produce the final output.

→ Output: [final deliverable]

--- STEP 4: Review (uses Step 3 output) ---
System: You are a critical reviewer. Check the output against the original
requirements and flag any gaps, errors, or improvements needed.

User:
<requirements>[original requirements]</requirements>
<output>[paste Step 3 output here]</output>

Review this output. Return: { "approved": boolean, "issues": [...] }

[EXAMPLE CHAIN — Blog Post Pipeline]
Step 1: Extract key points from a research document → JSON
Step 2: Turn key points into a blog outline → Markdown outline
Step 3: Write full blog post from outline → Full draft
Step 4: Edit for clarity and tone → Final draft

[NOTES]
- Keep each step's output structured (JSON, numbered list, markdown) so it's easy to pass forward.
- Add a "gate" step between major stages: validate the output before proceeding.
- Use different temperatures per step: 0 for extraction/planning, 0.7 for writing.
- If a step fails, you only need to re-run from that step — not the entire chain.
- For long chains, save intermediate outputs to avoid losing work.
```
