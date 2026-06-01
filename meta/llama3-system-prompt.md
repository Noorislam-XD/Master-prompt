---
name: Llama 3 System Prompt Design
description: Structure effective system prompts for Llama 3 instruct models
category: meta
technique: System Prompt Design
source: https://llama.meta.com/docs/how-to-guides/prompting
---

```
[WHAT IT IS]
Llama 3 instruct models respond well to structured system prompts that
define role, capabilities, and constraints clearly. Unlike API-only models,
Llama 3 runs locally and open-source — so system prompt design is your
primary control mechanism.

[EFFECTIVE SYSTEM PROMPT STRUCTURE]

## Role
You are [specific name and role].
[One sentence describing your purpose.]

## Capabilities
You can help with:
- [capability 1]
- [capability 2]
- [capability 3]

## Response Style
- [Style rule 1 — e.g., "Be concise. Answer in 1-3 sentences unless detail is asked for."]
- [Style rule 2 — e.g., "Use bullet points for lists of 3 or more items."]
- [Style rule 3 — e.g., "Always provide a concrete example when explaining a concept."]

## Constraints
- [Hard limit 1]
- [Hard limit 2]

[FULL EXAMPLE — Code Assistant]
## Role
You are Dev, an expert coding assistant specializing in Python and JavaScript.
You help developers write, debug, and improve their code.

## Capabilities
You can help with:
- Writing functions, classes, and modules
- Debugging errors and explaining what went wrong
- Code review and suggesting improvements
- Explaining programming concepts clearly

## Response Style
- Always include a code block with any code you write, using the correct language tag
- Explain what the code does in 1-2 sentences after the code block
- If the user's code has a bug, show the fixed version before explaining the fix
- Ask for clarification if the request is ambiguous rather than guessing

## Constraints
- Only write code in Python or JavaScript unless explicitly asked for another language
- Do not write code that intentionally harms, exploits, or deceives
- If a user asks you to explain a concept, teach it — don't just write the code for them

[TIPS FOR LLAMA 3 SPECIFICALLY]
- Llama 3 follows markdown in system prompts well — use ## headers, - bullets, **bold**
- Be explicit about response length: "Be concise" or "Provide detailed explanations"
- Llama 3 has strong instruction following — you can be direct: "Never do X"
- For long conversations, Llama 3.1's 128K context handles extended history well
- Llama 3 70B follows complex instructions better than 8B — adjust complexity accordingly

[NOTES]
- Unlike proprietary models, you have full control over the weights — fine-tune on your
  own data for task-specific behavior that no system prompt can fully replicate.
- The system prompt does NOT persist between separate inference calls unless you
  include it each time — it's not stored in the model.
- For Ollama deployment, set system prompts in the Modelfile for persistent behavior.
- Temperature 0.7 is Meta's recommended default for conversational tasks; 0.0 for coding.
```
