---
name: Response Prefilling
description: Control output format precisely by prefilling the start of Claude's response
category: anthropic
technique: Response Prefilling
source: https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/prefill-claudes-response
---

```
[WHAT IT IS]
Claude's API allows you to prefill the beginning of the assistant's response.
Claude continues from exactly where you left off — it cannot backtrack or add
a preamble. This is the most reliable way to enforce a specific output format.

[API USAGE — Python]
import anthropic

client = anthropic.Anthropic()

response = client.messages.create(
    model="claude-opus-4-5",
    max_tokens=1024,
    system="You are a JSON extraction engine.",
    messages=[
        {
            "role": "user",
            "content": "Extract the name and email from: 'Hi I'm John, reach me at john@example.com'"
        },
        {
            "role": "assistant",
            "content": "{"  # ← Prefill starts here. Claude continues from this point.
        }
    ]
)

print("{" + response.content[0].text)
# Output: {"name": "John", "email": "john@example.com"}

[USE CASES AND PREFILL VALUES]

--- Force JSON output (no markdown fences) ---
Prefill: "{"
Result: Claude returns raw JSON starting with {

--- Force a specific structure ---
Prefill: "## Summary\n"
Result: Claude starts directly with the Summary section

--- Prevent preamble ("Sure! Here's...") ---
Prefill: Any content — Claude cannot add a preamble before what you prefilled

--- Skip explanation, go straight to code ---
Prefill: "```python\n"
Result: Claude starts writing Python code immediately

--- Force a yes/no decision first ---
Prefill: "Decision: "
Result: Claude starts with "Decision: Yes" or "Decision: No"

--- XML output ---
Prefill: "<analysis>\n"
Result: Claude opens the tag and fills it in

[EXAMPLE — JSON with prefill]
System: Extract structured data. Return only valid JSON.

User: "Customer Sarah Chen ordered 3 units of Product X at $49 each on March 5."

Assistant (prefill): "{"

→ Claude continues: "{"name": "Sarah Chen", "quantity": 3, "product": "Product X", "unit_price": 49, "total": 147, "date": "March 5"}"

[NOTES]
- The prefill is included in your output — prepend it back when processing the response.
- Prefilling with "{" forces JSON and also prevents Claude from wrapping it in markdown fences.
- Do NOT prefill with "I " or affirmative phrases — this locks Claude into agreeing with whatever follows.
- Prefilling is Claude/Anthropic API-specific. Other providers may have equivalent features under different names.
- Use with XML tags for maximum format control: prefill "<output>" and instruct Claude to close the tag.
```
