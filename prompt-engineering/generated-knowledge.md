---
name: Generated Knowledge Prompting
description: Have the AI generate relevant background knowledge before answering
category: prompt-engineering
technique: Generated Knowledge
source: https://arxiv.org/abs/2110.08387
---

```
[WHAT IT IS]
Generated Knowledge Prompting asks the model to first generate relevant
background facts and principles before answering the actual question.
This gives the model an explicit "working memory" of relevant knowledge,
improving accuracy on commonsense and factual reasoning tasks.
Developed by Liu et al. (2022).

[TWO-STEP TEMPLATE]

Step 1 — Generate knowledge:
Generate [N] facts or principles that are relevant to answering this question.
Include only facts that are directly useful. Number each fact.

Question: [your question]

Step 2 — Use knowledge to answer:
Using the facts you generated above, now answer the question.
Cite which facts support your answer.

[SINGLE PROMPT VERSION]
Before answering, generate 5 relevant facts about this topic.
Then use those facts to answer the question. Label the two sections clearly.

Question: [your question]

RELEVANT FACTS:
1.
2.
3.
4.
5.

ANSWER (using the facts above):

[EXAMPLE]
Question: "Why do ships made of steel float even though steel is denser than water?"

RELEVANT FACTS:
1. Buoyancy is determined by the weight of water displaced, not the material's density alone (Archimedes' Principle).
2. A ship's hull is hollow — it displaces a large volume of water relative to its mass.
3. Steel has a density of ~7,800 kg/m³ vs water's 1,000 kg/m³.
4. The average density of the entire ship (steel + enclosed air) is less than 1,000 kg/m³.
5. If the ship's weight equals the weight of water it displaces, it floats.

ANSWER:
Steel ships float because of Archimedes' Principle [Fact 1]. Although steel is ~7.8x denser
than water [Fact 3], the ship's hollow hull displaces a large volume of water [Fact 2].
The average density of the whole ship — steel plus the large volume of air inside — is
less than water's density [Fact 4]. When the ship's weight equals the weight of the
displaced water, it floats [Fact 5].

[BEST USE CASES]
- Commonsense reasoning questions where the model may skip relevant context
- Science and factual questions where grounding helps accuracy
- Questions that seem simple but require applying non-obvious principles
- Any question where you notice the model jumping to conclusions

[NOTES]
- Generated Knowledge works because it forces the model to surface relevant
  context before committing to an answer — reducing confident wrong answers.
- Quality of generated facts matters: prompt for "relevant" and "directly useful"
  to avoid generic or irrelevant facts.
- Combine with CoT: generate knowledge → reason step by step → answer.
- For factual tasks, ask the model to rate its confidence in each generated fact.
- Works best with more capable models; smaller models may generate incorrect facts.
- Unlike RAG (which retrieves external facts), Generated Knowledge uses the model's
  parametric memory — so it can still hallucinate. Use RAG for verified facts.
```
