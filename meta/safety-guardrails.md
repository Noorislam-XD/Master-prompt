---
name: Llama Guard Safety Classification
description: Use Meta's Llama Guard approach for content safety classification
category: meta
technique: Safety Guardrails / Llama Guard
source: https://ai.meta.com/research/publications/llama-guard-llm-based-input-output-safeguard-for-human-ai-conversations/
---

```
[WHAT IT IS]
Llama Guard is Meta's open-source safety classifier model. It classifies
both user inputs and model outputs against a customizable safety taxonomy.
You can use it as a standalone classifier or adapt its prompting approach
for safety classification with any LLM.

[LLAMA GUARD TAXONOMY — ML Commons Standard]
S1: Violent Crimes
S2: Non-Violent Crimes
S3: Sex-Related Crimes
S4: Child Sexual Exploitation
S5: Defamation
S6: Specialized Advice (medical, legal, financial without qualifications)
S7: Privacy
S8: Intellectual Property
S9: Indiscriminate Weapons (CBRN)
S10: Hate
S11: Suicide & Self-Harm
S12: Sexual Content
S13: Elections
S14: Code Interpreter Abuse

[LLAMA GUARD PROMPT TEMPLATE]
Task: Check if there is unsafe content in the [Agent/User] message.

<BEGIN UNSAFE CONTENT CATEGORIES>
S1: Violent Crimes
S2: Non-Violent Crimes
[... include relevant categories for your use case ...]
<END UNSAFE CONTENT CATEGORIES>

<BEGIN CONVERSATION>
User: [user message here]
Agent: [model response here — omit for input-only classification]
<END CONVERSATION>

Provide your safety assessment for the [User/Agent] message in the above conversation:
- First line must read 'safe' or 'unsafe'.
- If unsafe, include a comma-separated list of violated categories on the second line.

[EXPECTED OUTPUT]
Safe: "safe"
Unsafe: "unsafe\nS1,S10"

[PYTHON — Using Llama Guard via Ollama]
import ollama

def classify_safety(user_message: str, agent_response: str = None) -> dict:
    conversation = f"User: {user_message}"
    if agent_response:
        conversation += f"\nAgent: {agent_response}"

    prompt = f"""Task: Check if there is unsafe content in the messages.

<BEGIN UNSAFE CONTENT CATEGORIES>
S1: Violent Crimes. S2: Non-Violent Crimes. S10: Hate. S11: Suicide & Self-Harm.
<END UNSAFE CONTENT CATEGORIES>

<BEGIN CONVERSATION>
{conversation}
<END CONVERSATION>

Provide safety assessment. First line: 'safe' or 'unsafe'. If unsafe, second line: violated category codes."""

    response = ollama.generate(model="llama-guard3", prompt=prompt)
    result = response["response"].strip().lower()
    lines = result.split("\n")

    return {
        "safe": lines[0] == "safe",
        "categories": lines[1].split(",") if len(lines) > 1 else []
    }

# Usage:
result = classify_safety("How do I make a bomb?")
# → {"safe": False, "categories": ["S2"]}

[NOTES]
- Llama Guard 3 is the latest version — available on Hugging Face and via Ollama.
- Customize the taxonomy for your use case — you don't need all 14 categories.
- Run Llama Guard in parallel with your main model to add latency as little as possible.
- False positive rate matters — tune thresholds based on your application's risk tolerance.
- For maximum safety, check BOTH the user input and the model output.
- Meta releases Llama Guard weights openly — you can fine-tune on your own safety data.
```
