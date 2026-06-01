# 📋 Changelog

All notable additions and updates to the Master Prompt Library are recorded here.

Format: `[version] — date — description`

---

## [1.5.0] — 2026-05-31

### Added — `/anthropic`
- `xml-tagging.md` — XML tags for structured, unambiguous Claude prompts
- `extended-thinking.md` — Claude extended thinking API for hard reasoning tasks
- `prompt-chaining.md` — Sequential sub-prompts with output handoffs
- `document-qa.md` — Document Q&A with precise citations
- `role-prompting.md` — Expert persona assignment for domain tasks
- `prefill.md` — Response prefilling to control output format precisely

### Added — `/google`
- `step-back.md` — Abstract to principles before solving specific questions
- `self-consistency.md` — Majority-vote across multiple reasoning paths
- `least-to-most.md` — Decompose hard problems into sequential sub-problems
- `multimodal.md` — Combine text + image inputs for vision tasks
- `system-instruction.md` — Gemini system instruction best practices
- `zero-shot-cot.md` — Trigger CoT reasoning with a single phrase

### Added — `/microsoft`
- `meta-prompt.md` — Prompt that generates optimized prompts for any task
- `grounding.md` — Anchor responses to trusted sources with Azure AI Search
- `safety-system-message.md` — Microsoft's recommended safety layer template
- `prompt-injection-defense.md` — Defend against adversarial instruction attacks
- `copilot-extension.md` — Microsoft 365 Copilot extension design

### Added — `/meta`
- `llama3-chat-template.md` — Official Llama 3 instruct message format
- `llama3-system-prompt.md` — Effective system prompt structure for Llama 3
- `code-llama.md` — Code Llama prompt formats for all variants
- `safety-guardrails.md` — Llama Guard safety classification approach

### Added — `/prompt-engineering`
- `react.md` — ReAct: interleaved reasoning and tool-use for agents
- `tree-of-thoughts.md` — Explore multiple reasoning branches simultaneously
- `self-refine.md` — Iterative output improvement through self-critique
- `automatic-prompt-engineer.md` — AI-generated and evaluated prompt optimization
- `directional-stimulus.md` — Subtle hints to guide without constraining
- `generated-knowledge.md` — Generate background facts before answering

---

## [1.4.0] — 2026-05-31

### Added — `/openai`
- `chain-of-thought.md` — Step-by-step reasoning before final answer
- `few-shot.md` — Teach by example with input/output pairs
- `structured-output.md` — Extract clean JSON from unstructured text
- `text-classification.md` — Classify text into predefined categories
- `summarization.md` — Multi-format document summarization
- `code-generation.md` — Reliable, production-ready code generation
- `function-calling.md` — Tool/function calling with schema definitions
- `rag-grounding.md` — Answer from retrieved context only, no hallucination
- `customer-service-agent.md` — Policy-following conversational support agent
- `content-moderation.md` — Safety classification by category and severity
- `persona.md` — Consistent character and knowledge boundary design
- `text-transformation.md` — Rewrite, translate, reformat, or change tone

---

## [1.3.0] — 2026-05-31

### Added
- `CONTRIBUTING.md` — Full contribution guide with prompt template, quality standards, PR checklist, and new category request process.

---

## [1.2.0] — 2026-05-31

### Added
- `SEARCH.md` — Full search index organized by goal, audience, and output format. Covers all 32 prompts across all 8 categories.

---

## [1.1.0] — 2026-05-31

### Added — `/coding`
- `senior-engineer.md` — General-purpose senior engineering persona
- `code-reviewer.md` — Structured PR and code review with severity tiers
- `debugger.md` — Root-cause debugging protocol
- `refactor-expert.md` — Safe, incremental refactoring
- `api-designer.md` — REST / GraphQL API design

### Added — `/business`
- `pitch-deck.md` — Investor pitch deck script writer
- `marketing-copy.md` — High-converting ad and landing page copy
- `business-plan.md` — Full business plan generator
- `competitive-analysis.md` — Market and competitor positioning

### Added — `/research`
- `deep-researcher.md` — Exhaustive topic research with citations
- `literature-review.md` — Academic literature review
- `fact-checker.md` — Claim verification and source auditing

### Added — `/writing`
- `technical-writer.md` — Clear, precise technical documentation
- `storyteller.md` — Narrative and long-form storytelling
- `editor.md` — Editing for clarity, tone, and flow
- `newsletter.md` — Engaging email newsletter writing

### Added — `/productivity`
- `meeting-notes.md` — Structured meeting notes with action items
- `sop-writer.md` — Standard Operating Procedure generation
- `task-planner.md` — Break goals into prioritized task lists
- `summarizer.md` — Summarize any document or transcript

### Added — `/education`
- `tutor.md` — Socratic tutor for any subject
- `curriculum-designer.md` — Full course or curriculum design
- `quiz-maker.md` — Multiple-choice and short-answer quiz generation
- `explainer.md` — Explain complex topics at any level

### Added — `/creative`
- `brainstormer.md` — Rapid divergent idea generation
- `world-builder.md` — Fictional world and lore creation
- `design-brief.md` — Creative direction and design brief writing
- `naming-expert.md` — Product, brand, or feature naming

### Added — `/agents`
- `software-factory.md` — 7-agent software development pipeline
- `research-pipeline.md` — Multi-step research and synthesis pipeline
- `content-pipeline.md` — Automated content creation workflow
- `qa-agent.md` — Autonomous QA and testing agent

---

## [1.0.0] — 2026-05-31

### Added
- Initial repository structure with 8 category folders
- Root `README.md` with navigator prompt and usage guide
- Category `README.md` files with prompt tables and contribution template

---

## How to Update This File

When you add or change a prompt, add an entry under a new version heading:

```markdown
## [X.Y.Z] — YYYY-MM-DD

### Added
- `category/filename.md` — one-line description

### Changed
- `category/filename.md` — what was updated and why

### Removed
- `category/filename.md` — why it was removed
```

**Version numbering:**
- `MAJOR` (X) — restructure of categories or breaking changes to the template format
- `MINOR` (Y) — new prompt files added
- `PATCH` (Z) — edits, fixes, or improvements to existing prompts
