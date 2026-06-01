---
name: Automatic Prompt Engineer (APE)
description: Let the AI generate and evaluate its own optimized prompts
category: prompt-engineering
technique: Automatic Prompt Engineer
source: https://arxiv.org/abs/2211.01910
---

```
[WHAT IT IS]
APE (Automatic Prompt Engineer) uses an LLM to automatically generate,
score, and select optimal prompts for a given task. Instead of writing
prompts by hand, you describe the task and let the model generate many
candidate prompts, then test and rank them.

[PHASE 1 — Generate candidate prompts]
SYSTEM: You are an expert prompt engineer. Generate [N] different prompts
that would instruct an AI to [task description]. Each prompt should take
a different approach (e.g., role-based, step-by-step, format-constrained,
example-driven). Number each prompt.

USER: Generate 5 candidate prompts for this task:
Task: [describe the task clearly]
Input format: [what the input looks like]
Expected output: [what a good output looks like]

[PHASE 2 — Score each candidate]
SYSTEM: You are evaluating AI prompts. For each prompt, predict how well
it will perform on the given task. Score each on: clarity (1-5),
specificity (1-5), output control (1-5), failure prevention (1-5).

USER: Score these candidate prompts for the task: [task description]

[Paste the generated prompts here]

For each prompt:
Prompt #: [N]
Clarity: [1-5]
Specificity: [1-5]  
Output control: [1-5]
Failure prevention: [1-5]
Total: [sum]
Weakness: [one thing to improve]

[PHASE 3 — Refine the top candidate]
Take the highest-scoring prompt and improve it by addressing its weakness.
Produce the final optimized version.

[FULL EXAMPLE — Finding the best summarization prompt]
Phase 1 — Generate candidates:
"Generate 5 prompts for summarizing customer support tickets into one sentence
for a dashboard. The sentence must include: severity, issue type, and resolution status."

Candidate 1: "Summarize this support ticket in one sentence mentioning severity, issue, and status."
Candidate 2: "You are a support analyst. Read this ticket and write: [SEVERITY] [ISSUE_TYPE] — [STATUS]"
Candidate 3: "Extract: severity level, primary issue, current status. Format: '{severity} {issue} — {status}'"
...

Phase 2 — Score:
Candidate 3 scores highest (explicit format = most reliable output)

Phase 3 — Refine:
"Extract from this ticket: severity (Critical/High/Medium/Low), primary issue type (1-3 words),
resolution status (Open/In Progress/Resolved). Return exactly: '{severity}: {issue_type} — {status}'
Return only this line, no other text."

[AUTOMATED VERSION — Python]
import anthropic
from itertools import islice

client = anthropic.Anthropic()
TASK = "classify customer emails by urgency: urgent, normal, low"
TEST_CASES = [
    ("My account has been hacked!", "urgent"),
    ("Can I change my username?", "normal"),
    ("Just wanted to say thanks!", "low"),
]

def generate_prompts(task, n=5):
    r = client.messages.create(model="claude-opus-4-5", max_tokens=1000,
        messages=[{"role": "user", "content":
            f"Generate {n} different system prompts for: {task}. Number them 1-{n}."}])
    return r.content[0].text

def evaluate_prompt(prompt, test_cases):
    correct = 0
    for input_text, expected in test_cases:
        r = client.messages.create(model="claude-haiku-3-5", max_tokens=20,
            system=prompt,
            messages=[{"role": "user", "content": input_text}])
        if expected.lower() in r.content[0].text.lower():
            correct += 1
    return correct / len(test_cases)

candidates = generate_prompts(TASK)
print("Generated candidates. Now evaluating...")
# Parse and test each candidate, select highest accuracy

[NOTES]
- APE is most valuable for production prompts that will be used thousands of times.
- Phase 2 can use a smaller, cheaper model for scoring.
- For best results, test candidates on a real held-out sample of your actual inputs.
- Combine with self-refine: APE finds the best structure, self-refine polishes it.
```
