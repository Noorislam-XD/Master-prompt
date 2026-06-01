---
name: Self-Refine
description: Iteratively improve AI output through self-critique and revision
category: prompt-engineering
technique: Self-Refine
source: https://arxiv.org/abs/2303.17651
---

```
[WHAT IT IS]
Self-Refine is a technique where the model generates an initial output,
critiques its own output against specific criteria, then revises it.
Multiple refinement cycles compound improvements. Works without human
feedback. Developed at CMU.

[THREE-STEP FORMAT]

Step 1 — Generate:
[Task instruction]

Step 2 — Critique:
Review your output above. Evaluate it against these criteria:
- [Criterion 1: e.g., "Is it accurate and factually correct?"]
- [Criterion 2: e.g., "Is it clear and easy to understand?"]
- [Criterion 3: e.g., "Does it directly address what was asked?"]
- [Criterion 4: e.g., "Is it an appropriate length?"]

List specific improvements needed. Be harsh — this is a first draft.

Step 3 — Refine:
Rewrite the output, addressing every issue you identified in your critique.

[COMPLETE SINGLE PROMPT — Copy & Use]
Complete this task, then critique your work, then produce an improved final version.

TASK: [your task here]

---
INITIAL DRAFT:
[Generate the output]

---
CRITIQUE:
Review your draft above. For each criterion below, note specific problems:
1. Accuracy — any errors or unsupported claims?
2. Clarity — anything confusing or vague?
3. Completeness — anything missing that should be included?
4. Conciseness — anything that could be cut without losing value?
5. Format — is the structure appropriate for the task?

---
REVISED VERSION:
[Rewrite addressing all issues from the critique]

[MULTI-CYCLE PYTHON VERSION]
import anthropic

client = anthropic.Anthropic()
task = "Write a persuasive argument for a 4-day work week"

def generate(task):
    r = client.messages.create(model="claude-opus-4-5", max_tokens=500,
        messages=[{"role": "user", "content": task}])
    return r.content[0].text

def critique(output, criteria):
    prompt = f"Critique this output against: {criteria}\n\nOutput:\n{output}\n\nList specific issues only."
    r = client.messages.create(model="claude-opus-4-5", max_tokens=300,
        messages=[{"role": "user", "content": prompt}])
    return r.content[0].text

def refine(output, issues):
    prompt = f"Rewrite this, fixing these issues:\n{issues}\n\nOriginal:\n{output}"
    r = client.messages.create(model="claude-opus-4-5", max_tokens=500,
        messages=[{"role": "user", "content": prompt}])
    return r.content[0].text

current = generate(task)
for cycle in range(3):  # 3 refinement cycles
    issues = critique(current, "accuracy, clarity, persuasiveness, evidence")
    current = refine(current, issues)
    print(f"Cycle {cycle+1} complete")

print("Final output:", current)

[BEST USE CASES]
- Writing tasks (emails, essays, documentation)
- Code review and improvement
- Arguments, proposals, and plans
- Any creative task where a first draft is likely imperfect

[NOTES]
- Specify concrete criteria in the critique step — "make it better" produces weak critiques.
- 2-3 cycles is the sweet spot; diminishing returns after that.
- The critique quality depends heavily on the criteria you define.
- Self-Refine works best for style and structure improvements; less effective for
  factual corrections where the model confidently holds wrong beliefs.
- Cost: each cycle = 2 additional API calls (critique + refine). Budget accordingly.
```
