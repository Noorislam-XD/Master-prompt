---
name: Grounding with Sources
description: Anchor AI responses to trusted data sources to eliminate hallucination
category: microsoft
technique: Grounding
source: https://learn.microsoft.com/en-us/azure/ai-services/openai/concepts/grounding
---

```
[WHAT IT IS]
Grounding connects the model's responses to specific, trusted data sources
(documents, databases, search results). It's the foundation of enterprise AI
deployments. Microsoft uses it extensively in Copilot and Azure AI Search.

[SYSTEM PROMPT TEMPLATE]
You are a [role] assistant for [company/domain].

Grounding rules — you must follow these without exception:
1. Only use information from the SOURCES provided to you.
2. If the answer is not in the sources, say: "I don't have that information
   in my current knowledge base. You may want to [suggest next step]."
3. Always cite your source after each factual claim using [Source: Title].
4. Never combine source information with your own knowledge to fill gaps.
5. If sources conflict, present both and note the conflict.

[USER PROMPT TEMPLATE — with injected sources]
SOURCES:
---
Source 1: [Title]
[Content]
---
Source 2: [Title]
[Content]
---

USER QUESTION: [question]

[GROUNDING ARCHITECTURE — Azure AI Search + OpenAI]
# Conceptual flow for developers:

# 1. User submits query
query = "What is the refund policy for digital products?"

# 2. Retrieve relevant chunks via Azure AI Search
search_results = azure_search.search(query, top=3)

# 3. Format sources for injection
sources_text = "\n---\n".join([
    f"Source {i+1}: {r['title']}\n{r['content']}"
    for i, r in enumerate(search_results)
])

# 4. Build grounded prompt
system = """You are a customer support agent.
Only use the SOURCES provided. Cite each source you use.
If the answer isn't in the sources, say so clearly."""

user_message = f"SOURCES:\n{sources_text}\n\nQUESTION: {query}"

# 5. Call the model with grounded context
response = openai.chat.completions.create(
    model="gpt-4o",
    messages=[
        {"role": "system", "content": system},
        {"role": "user", "content": user_message}
    ]
)

[EXAMPLE]
Source 1: Return Policy (updated 2024-03)
"Digital products are non-refundable once downloaded. Physical products may
be returned within 30 days with original receipt."

Question: "Can I get a refund on an app I downloaded yesterday?"

Grounded response:
"Digital products are non-refundable once downloaded [Source: Return Policy].
Since you've already downloaded the app, it would not qualify for a refund
under the current policy. I'd recommend contacting support to discuss your
specific situation."

[NOTES]
- Chunk size of 512–1024 tokens balances retrieval relevance and context coverage.
- Reranking search results before injection improves answer quality significantly.
- For production: log all "not in sources" responses to identify knowledge base gaps.
- Hybrid search (keyword + semantic/vector) outperforms either alone for grounding.
- Microsoft's Responsible AI guidelines recommend grounding for all enterprise deployments.
```
