# 🤖 OpenAI Prompt Packs

Prompts based on OpenAI's publicly documented best practices, the [OpenAI Cookbook](https://cookbook.openai.com), and the official [Prompt Engineering Guide](https://platform.openai.com/docs/guides/prompt-engineering). Each file demonstrates a core prompting technique recommended by OpenAI.

## Prompts in this folder

| File | Technique | Use Case |
|------|-----------|----------|
| [`chain-of-thought.md`](./chain-of-thought.md) | Chain-of-Thought | Step-by-step reasoning for complex problems |
| [`few-shot.md`](./few-shot.md) | Few-Shot Prompting | Teach the model by example |
| [`structured-output.md`](./structured-output.md) | Structured Output | Extract clean JSON from unstructured text |
| [`text-classification.md`](./text-classification.md) | Classification | Categorize text into defined labels |
| [`summarization.md`](./summarization.md) | Summarization | Condense documents at any length or detail level |
| [`code-generation.md`](./code-generation.md) | Code Generation | Generate reliable, well-commented code |
| [`function-calling.md`](./function-calling.md) | Tool / Function Calling | Define tools the model can invoke |
| [`rag-grounding.md`](./rag-grounding.md) | RAG / Context Grounding | Answer from retrieved context only |
| [`customer-service-agent.md`](./customer-service-agent.md) | Conversational Agent | Consistent, policy-following support agent |
| [`content-moderation.md`](./content-moderation.md) | Moderation | Classify content by safety category |
| [`persona.md`](./persona.md) | Persona / Character | Maintain a consistent character across a conversation |
| [`text-transformation.md`](./text-transformation.md) | Text Transformation | Rewrite, translate, or reformat any text |

## Prompt Template

```
---
name:
description:
category: openai
technique:
source:
---

[SYSTEM PROMPT]
...

[USER PROMPT TEMPLATE]
...

[EXAMPLE INPUT]
...

[EXAMPLE OUTPUT]
...

[NOTES]
...
```
