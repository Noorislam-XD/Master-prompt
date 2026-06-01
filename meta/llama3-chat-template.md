---
name: Llama 3 Chat Template
description: Correct Llama 3 instruct model message format for reliable responses
category: meta
technique: Chat Template
source: https://llama.meta.com/docs/model-cards-and-prompt-formats/meta-llama-3/
---

```
[WHAT IT IS]
Llama 3 instruct models require a specific chat template format using special
tokens. Using the wrong format causes degraded performance or nonsensical outputs.
This is the official Meta format for Llama 3.1 and 3.2 instruct models.

[OFFICIAL LLAMA 3 FORMAT]
<|begin_of_text|>
<|start_header_id|>system<|end_header_id|>

[Your system prompt here]
<|eot_id|>
<|start_header_id|>user<|end_header_id|>

[User message here]
<|eot_id|>
<|start_header_id|>assistant<|end_header_id|>

[SPECIAL TOKENS]
<|begin_of_text|>   → Start of the entire prompt
<|start_header_id|> → Opens a role header
<|end_header_id|>   → Closes a role header
<|eot_id|>          → End of a turn (End Of Turn)
Roles: system | user | assistant | tool (for function calling)

[COMPLETE MULTI-TURN EXAMPLE]
<|begin_of_text|>
<|start_header_id|>system<|end_header_id|>

You are a helpful assistant. Be concise and accurate.
<|eot_id|>
<|start_header_id|>user<|end_header_id|>

What is the capital of France?
<|eot_id|>
<|start_header_id|>assistant<|end_header_id|>

Paris.
<|eot_id|>
<|start_header_id|>user<|end_header_id|>

And what is its population?
<|eot_id|>
<|start_header_id|>assistant<|end_header_id|>

[PYTHON — Using transformers tokenizer (recommended)]
from transformers import AutoTokenizer

tokenizer = AutoTokenizer.from_pretrained("meta-llama/Meta-Llama-3.1-8B-Instruct")

messages = [
    {"role": "system", "content": "You are a helpful assistant."},
    {"role": "user", "content": "What is the capital of France?"}
]

# apply_chat_template handles the format automatically
formatted = tokenizer.apply_chat_template(
    messages,
    tokenize=False,
    add_generation_prompt=True  # Adds the final assistant header
)
print(formatted)

[PYTHON — Using Ollama (local inference)]
import ollama

response = ollama.chat(
    model="llama3.1",
    messages=[
        {"role": "system", "content": "You are a helpful assistant."},
        {"role": "user", "content": "What is the capital of France?"}
    ]
)
print(response["message"]["content"])

[NOTES]
- Always use apply_chat_template when using the HuggingFace transformers library —
  it handles the special tokens correctly and updates automatically for new models.
- The final <|start_header_id|>assistant<|end_header_id|> without <|eot_id|>
  is the "generation prompt" — it tells the model to start generating the response.
- Omitting special tokens with instruct models causes the model to generate
  repetitive, low-quality, or off-format responses.
- Llama 3 Base (non-instruct) does NOT use this template — it's for completion only.
- For tool calling, add role "tool" turns between assistant and user turns.
```
