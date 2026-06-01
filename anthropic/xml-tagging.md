---
name: XML Tagging for Structure
description: Use XML tags to clearly separate instructions, inputs, and outputs for Claude
category: anthropic
technique: XML Structure
source: https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/use-xml-tags
---

```
[WHY XML TAGS]
Claude is trained to pay close attention to XML tags. Using them to separate
distinct parts of your prompt dramatically reduces ambiguity, prevents content
from one section bleeding into another, and makes complex prompts easier to
maintain.

[SYSTEM PROMPT TEMPLATE]
You are a [role]. You will be given a [document/context/task] inside <input> tags
and instructions inside <instructions> tags. Produce your response inside
<output> tags.

Rules:
- Only use information from within the <input> tags.
- Follow only the instructions in the <instructions> tags.
- Always wrap your entire response in <output></output>.

[USER PROMPT TEMPLATE]
<instructions>
[What you want Claude to do]
</instructions>

<input>
[The text, document, or data to process]
</input>

[EXAMPLE — Summarize + Extract]
System: You are a document analyst. Summarize the document and extract all
action items. Wrap your summary in <summary> and action items in <actions>.

User:
<instructions>
Summarize this email and list all action items assigned to me (Sarah).
</instructions>

<input>
Hi Sarah,

Following up on yesterday's meeting. Please review the Q3 budget by Friday and
send your comments to finance@company.com. John will handle the slide deck.
Also, can you book the conference room for next Tuesday at 2pm?

Thanks,
Mark
</input>

[EXAMPLE OUTPUT]
<summary>
Mark is following up on a meeting with two tasks for Sarah: reviewing the Q3
budget and booking a conference room.
</summary>

<actions>
1. Review the Q3 budget and email comments to finance@company.com by Friday.
2. Book the conference room for next Tuesday at 2pm.
</actions>

[NOTES]
- Use semantic tag names that describe the content: <document>, <rules>, <example>, <output> — not generic names like <tag1>.
- Tags make it easy to inject dynamic content into prompts programmatically: f"<document>{user_text}</document>"
- For multi-document prompts, number tags: <document_1>, <document_2>, etc.
- Claude can be instructed to produce output in specific XML tags, making parsing deterministic.
- Avoid nesting more than 2-3 levels deep — it adds cognitive load without benefit.
```
