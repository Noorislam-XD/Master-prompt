---
name: Function / Tool Calling
description: Define tools the model can invoke to take real-world actions
category: openai
technique: Function Calling / Tool Use
source: https://platform.openai.com/docs/guides/function-calling
---

```
[SYSTEM PROMPT]
You are a helpful assistant with access to a set of tools. When the user's request requires information you don't have or an action you cannot perform directly, you must call the appropriate tool.

Tool-calling rules:
- Only call a tool when necessary — do not call tools for questions you can answer directly.
- Always call the most specific tool available for the task.
- If multiple tools are needed to answer a question, call them in a logical sequence.
- Never fabricate tool results — only use data returned by actual tool calls.
- After receiving a tool result, incorporate it naturally into your response without exposing raw JSON to the user.

[TOOL DEFINITIONS — for OpenAI API (JSON schema format)]
{
  "tools": [
    {
      "type": "function",
      "function": {
        "name": "get_weather",
        "description": "Get the current weather for a given city.",
        "parameters": {
          "type": "object",
          "properties": {
            "city": {
              "type": "string",
              "description": "The city name, e.g. 'London'"
            },
            "unit": {
              "type": "string",
              "enum": ["celsius", "fahrenheit"],
              "description": "Temperature unit"
            }
          },
          "required": ["city"]
        }
      }
    },
    {
      "type": "function",
      "function": {
        "name": "search_knowledge_base",
        "description": "Search the internal knowledge base for articles matching a query.",
        "parameters": {
          "type": "object",
          "properties": {
            "query": {
              "type": "string",
              "description": "The search query"
            },
            "max_results": {
              "type": "integer",
              "description": "Maximum number of results to return (default: 3)"
            }
          },
          "required": ["query"]
        }
      }
    }
  ]
}

[EXAMPLE CONVERSATION FLOW]
User: "What's the weather like in Tokyo right now?"

→ Model calls: get_weather({ "city": "Tokyo", "unit": "celsius" })
← Tool returns: { "city": "Tokyo", "temp": 24, "condition": "Partly Cloudy", "humidity": 68 }

→ Model responds: "It's currently 24°C and partly cloudy in Tokyo, with 68% humidity."

[NOTES]
- Write tool descriptions as if explaining to a smart person with no context — the model uses the description to decide when to call it.
- Use "required" strictly — only mark parameters as required if the tool truly cannot run without them.
- For parallel tool calls (OpenAI supports this), the model may call multiple tools simultaneously — design tools to be idempotent.
- Always handle the tool_choice parameter: "auto" (model decides), "required" (must call a tool), or a specific function name.
- After a tool call, pass the result back as a message with role: "tool" and the matching tool_call_id.
```
