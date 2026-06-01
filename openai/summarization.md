---
name: Summarization
description: Condense any document at a specified length and detail level
category: openai
technique: Summarization
source: https://platform.openai.com/docs/guides/prompt-engineering#strategy-specify-the-desired-length
---

```
[SYSTEM PROMPT]
You are a professional summarization engine. You produce accurate, concise summaries that preserve the most important information without introducing anything not present in the original text.

Summarization rules:
- Never add opinions, context, or facts not present in the source text.
- Preserve all key figures, dates, names, and decisions.
- Match the requested output format exactly.
- If the source contains contradictions, flag them rather than silently resolving them.

[USER PROMPT TEMPLATE — One Sentence]
Summarize the following text in exactly one sentence:

"""
[Text here]
"""

[USER PROMPT TEMPLATE — Bullet Points]
Summarize the following text as 5 bullet points, ordered from most to least important:

"""
[Text here]
"""

[USER PROMPT TEMPLATE — Executive Brief]
Summarize the following text for a senior executive who has 30 seconds to read it. Include: the situation, the key decision or finding, and the recommended action (if any).

"""
[Text here]
"""

[USER PROMPT TEMPLATE — Layered Summary]
Summarize the following text at three levels:
1. One sentence (for a tweet)
2. One paragraph (for a colleague)
3. Five bullet points (for a report)

"""
[Text here]
"""

[EXAMPLE INPUT — Bullet Points]
Summarize the following text as 5 bullet points, ordered from most to least important:

"""
OpenAI released GPT-4 in March 2023. It is a multimodal model capable of accepting both image and text inputs. GPT-4 outperforms GPT-3.5 on a variety of professional and academic benchmarks, including scoring in the top 10% on the Uniform Bar Exam. The model is available via ChatGPT Plus and the OpenAI API. Safety mitigations were developed over six months prior to release.
"""

[EXAMPLE OUTPUT]
• GPT-4 is a multimodal model accepting text and image inputs, released March 2023.
• It scores in the top 10% on the Uniform Bar Exam and outperforms GPT-3.5 on academic benchmarks.
• Available through ChatGPT Plus and the OpenAI API.
• Six months of safety work preceded the public release.
• Marks a significant capability jump over the previous GPT-3.5 generation.

[NOTES]
- Specifying exact length (word count, sentence count, bullet count) produces more consistent results than vague instructions like "brief" or "short."
- For long documents, use a map-reduce approach: chunk → summarize each chunk → summarize the summaries.
- "Extractive" vs "abstractive": instruct the model to use only the source's own words when you need high fidelity.
```
