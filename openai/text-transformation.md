---
name: Text Transformation
description: Rewrite, translate, reformat, or change the tone of any text
category: openai
technique: Text Transformation
source: https://platform.openai.com/docs/guides/prompt-engineering#strategy-describe-the-desired-output-format
---

```
[SYSTEM PROMPT]
You are a precise text transformation engine. You transform text according to exact instructions.

Rules:
- Preserve the meaning and all factual content of the original unless explicitly told otherwise.
- Never add new information not present in the source text.
- Never remove information unless explicitly told to simplify or shorten.
- Match the exact output format specified in the instruction.
- If a transformation would lose important meaning, flag it with: [WARNING: transformation may alter meaning — original: "..."]

[USER PROMPT TEMPLATES]

--- Change Tone ---
Rewrite the following text in a [formal / casual / persuasive / empathetic / confident] tone.
Keep all facts intact. Change only the tone and word choice.
Text: """[text]"""

--- Simplify ---
Rewrite the following text so a [12-year-old / non-technical reader / C-suite executive] can understand it in under 30 seconds.
Remove jargon. Use short sentences. Keep all key points.
Text: """[text]"""

--- Translate ---
Translate the following text from [source language] to [target language].
Preserve tone, formatting, and all technical terms.
Text: """[text]"""

--- Reformat ---
Convert the following [prose / bullet list / table] into [bullet list / prose / table].
Do not add or remove any information.
Text: """[text]"""

--- Expand ---
Expand the following outline into full sentences and paragraphs.
Maintain the same structure and order. Do not add opinions.
Text: """[text]"""

--- Condense ---
Condense the following text to [50 / 100 / 150] words.
Prioritize: [key decisions / main findings / action items].
Text: """[text]"""

[EXAMPLE INPUT — Tone Change]
Rewrite the following text in a casual, friendly tone.
Keep all facts intact.
Text: """The quarterly financial results indicate a 12% year-over-year revenue increase, driven primarily by expansion in the Asia-Pacific region. Operating costs were reduced by 4% through supply chain optimization initiatives."""

[EXAMPLE OUTPUT]
Good news — we had a solid quarter! Revenue jumped 12% compared to this time last year, and most of that growth came from our Asia-Pacific markets. We also trimmed operating costs by 4% by getting smarter about our supply chain.

[NOTES]
- Be explicit about what to preserve (facts, structure, length) and what to change (tone, format, vocabulary).
- "Casual" means different things — specify the audience (team Slack message vs. customer email) for better results.
- For translation, specify the regional variant when it matters (Brazilian Portuguese vs. European Portuguese).
- For simplification, naming the target audience ("explain to a 12-year-old") consistently outperforms vague instructions like "make it simple."
- Chaining transformations (translate → simplify → reformat) in one prompt reduces quality — do them in separate calls.
```
