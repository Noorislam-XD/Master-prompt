---
name: ReAct (Reason + Act)
description: Interleave reasoning and actions for reliable AI agent tasks
category: prompt-engineering
technique: ReAct
source: https://arxiv.org/abs/2210.03629
---

```
[WHAT IT IS]
ReAct (Reasoning + Acting) is a prompting technique where the model alternates
between Thought (reasoning about what to do), Action (calling a tool or taking
a step), and Observation (processing the result). Developed by Google and
Princeton. The foundation of most modern AI agent frameworks.

[REACHT LOOP FORMAT]
Thought: [What do I need to figure out or do next?]
Action: [tool_name(parameters)]
Observation: [Result from the tool/action]
Thought: [What does this result tell me? What's next?]
Action: [next action]
Observation: [result]
...
Thought: [I now have enough information to answer]
Final Answer: [complete answer to the original question]

[SYSTEM PROMPT]
You are a helpful agent that solves problems by reasoning and using tools.

You have access to the following tools:
- search(query: str) → Returns web search results
- calculator(expression: str) → Evaluates a math expression
- lookup(topic: str) → Looks up a specific fact

Use this exact format for every step:
Thought: [your reasoning about what to do next]
Action: [tool_name(parameters)]
Observation: [result of the action — provided by the system]

When you have the final answer, write:
Thought: I now have all the information I need.
Final Answer: [your complete answer]

Do not skip steps. Do not guess. If a tool doesn't give you what you need,
reason about why and try a different approach.

[EXAMPLE]
Question: "What is the current population of Tokyo, and how many times larger
is it than the population of Paris?"

Thought: I need the current population of Tokyo and Paris to answer this.
Action: search("current population of Tokyo 2024")
Observation: Tokyo's population is approximately 13.96 million (city proper) or 37.4 million (greater metro area) as of 2024.

Thought: I'll use the city proper figure. Now I need Paris's population.
Action: search("current population of Paris 2024")
Observation: Paris city proper has a population of approximately 2.16 million as of 2024.

Thought: Now I can calculate the ratio.
Action: calculator(13.96 / 2.16)
Observation: 6.46

Thought: I have all the information I need.
Final Answer: Tokyo's city proper population is approximately 13.96 million people. This is about 6.5 times larger than Paris's city proper population of approximately 2.16 million.

[NOTES]
- ReAct significantly reduces hallucination compared to asking the model to
  answer without tool access — it externalizes memory and computation.
- The Thought step is critical — it forces the model to reason before acting,
  preventing random tool calls.
- Implemented in LangChain (create_react_agent), LlamaIndex, and most agent frameworks.
- For production: add a max_iterations limit to prevent infinite loops.
- "Observation" content comes from actual tool execution — never let the model
  write its own Observations.
```
