# 📋 Changelog

All notable additions and updates to the Master Prompt Library are recorded here.

Format: `[version] — date — description`

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
