---
name: Code Llama Prompt Format
description: Correct prompt format for Meta's Code Llama models for programming tasks
category: meta
technique: Code Generation
source: https://github.com/meta-llama/codellama
---

```
[WHAT IT IS]
Code Llama is Meta's family of code-specialized models fine-tuned from
Llama 2. It comes in three variants: base (completion), instruct (follows
instructions), and infilling (fills in code gaps). Each requires a
different prompt format.

[MODEL VARIANTS]
- CodeLlama-[7/13/34/70]b       → Base: code completion
- CodeLlama-[7/13/34/70]b-Instruct → Instruct: follows natural language instructions
- CodeLlama-[7/13/34/70]b-Python → Python-specialized
- Llama 3.1 is now preferred for code tasks — better general capability

[INSTRUCT FORMAT]
<s>[INST] {user_message} [/INST]

Multi-turn:
<s>[INST] {message_1} [/INST] {response_1} </s><s>[INST] {message_2} [/INST]

With system prompt:
<s>[INST] <<SYS>>
{system_message}
<</SYS>>

{user_message} [/INST]

[INFILLING FORMAT — Fill in the Middle]
<PRE> {prefix code} <SUF> {suffix code} <MID>

Example:
<PRE> def calculate_average(numbers):
    total = <SUF>
    return total / len(numbers) <MID>

→ Model fills in: sum(numbers)

[PYTHON — Code generation with transformers]
from transformers import AutoTokenizer, AutoModelForCausalLM
import torch

model_id = "codellama/CodeLlama-7b-Instruct-hf"
tokenizer = AutoTokenizer.from_pretrained(model_id)
model = AutoModelForCausalLM.from_pretrained(model_id, torch_dtype=torch.float16)

prompt = """<s>[INST] Write a Python function that reads a CSV file and returns
a dictionary mapping each unique value in a specified column to the count
of its occurrences. Include error handling for missing files. [/INST]"""

inputs = tokenizer(prompt, return_tensors="pt")
output = model.generate(**inputs, max_new_tokens=500, temperature=0.2)
print(tokenizer.decode(output[0], skip_special_tokens=True))

[SYSTEM PROMPT FOR CODE TASKS]
<s>[INST] <<SYS>>
You are an expert software engineer. When writing code:
- Write complete, runnable code only — no pseudocode
- Add docstrings for all functions
- Handle errors explicitly with try/except
- Use type hints for Python code
- After code, add a one-line "# Usage:" comment showing how to call it
<</SYS>>

{coding task here} [/INST]

[NOTES]
- For most new projects, use Llama 3.1 instead of Code Llama — it has better
  code performance and a larger context window (128K vs 100K).
- Code Llama Python variant outperforms the base model on Python-only tasks.
- Temperature 0.1–0.2 for code generation (low creativity needed, high precision).
- The infilling format is unique to Code Llama — no equivalent in base Llama models.
- Ollama supports Code Llama: `ollama run codellama:7b-instruct`
```
