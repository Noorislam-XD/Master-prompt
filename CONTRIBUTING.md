# 🤝 Contributing to the Master Prompt Library

Thanks for wanting to contribute! This library grows better with every prompt added. Here's how to do it right.

---

## Quick Start

1. Fork this repository.
2. Create a new branch: `git checkout -b add/your-prompt-name`
3. Add your prompt file inside the correct category folder.
4. Update the category `README.md` to list your new prompt.
5. Add your prompt to [`SEARCH.md`](./SEARCH.md) under the relevant sections.
6. Open a pull request with a short description of what the prompt does.

---

## Prompt File Template

Every prompt must be a `.md` file with this exact structure:

````markdown
---
name: Your Prompt Name
description: One sentence describing what this prompt does
category: coding | business | research | writing | productivity | education | creative | agents
---

```
[ROLE]
You are a [specific expert role with relevant experience/background].

[CONTEXT]
[Background the AI needs. Who is the audience? What is the situation? What are the stakes?]

[TASK]
[Numbered or structured list of what the AI must do, step by step.]

[FORMAT]
[Exactly how the output should be structured — headers, tables, code blocks, etc.]

[CONSTRAINTS]
- [What the AI must never do]
- [Hard limits on behavior or output]
- [Common failure modes to prevent]

[EXAMPLE]
[A brief before/after or sample output showing what "good" looks like]
```
````

---

## Prompt Quality Standards

Your prompt will be accepted if it meets all of these:

### ✅ The Role is specific
- ❌ "You are an expert."
- ✅ "You are a Senior Backend Engineer with 10+ years of experience in distributed systems."

### ✅ The Task is structured and complete
- ❌ "Help me write better code."
- ✅ Numbered steps with a clear start and end state.

### ✅ The Format is defined
- The AI should know exactly what structure to produce.
- Include headers, table layouts, or code block examples where relevant.

### ✅ The Constraints prevent failure
- Every prompt has a most common failure mode. Your constraints must address it.
- At least 3 constraints required.

### ✅ The Example shows the bar
- An example of what a correct output looks like (or a before/after showing improvement).
- Does not need to be exhaustive — just enough to calibrate the AI.

---

## Choosing the Right Category

| Category | Belongs here if... |
|----------|-------------------|
| `/coding` | The output is code, architecture, or engineering decisions |
| `/business` | The output is strategy, marketing, finance, or operations |
| `/research` | The output is analysis, synthesis, or verified information |
| `/writing` | The output is prose — articles, docs, stories, emails |
| `/productivity` | The output helps organize, plan, or process information |
| `/education` | The output teaches, explains, or assesses learning |
| `/creative` | The output generates ideas, concepts, or creative work |
| `/agents` | The prompt defines a multi-step or multi-agent workflow |

If your prompt spans two categories, pick the one that best describes the **primary output**.

---

## Updating SEARCH.md

Add your prompt to at least **two sections** in `SEARCH.md`:

1. The most relevant **By Goal** table row.
2. The most relevant **By Audience** list.
3. Optionally, the **By Format Output** table if it produces a distinctive format.

Format for a new table row:
```markdown
| What the user wants to do | Your Prompt Name | [category/filename.md](./category/filename.md) |
```

---

## What We Won't Accept

- **Prompts without all 6 sections** (`[ROLE]`, `[CONTEXT]`, `[TASK]`, `[FORMAT]`, `[CONSTRAINTS]`, `[EXAMPLE]`)
- **Vague roles** — "You are an expert" with no domain, seniority, or context
- **Tasks without structure** — a task must have clear steps or criteria
- **Duplicate prompts** — check the existing library before submitting
- **Prompts that ask the AI to deceive, manipulate, or cause harm**
- **Prompts that include personal data, API keys, or credentials**

---

## Pull Request Checklist

Before opening a PR, confirm:

- [ ] Prompt file is in the correct category folder
- [ ] File is named in `kebab-case.md`
- [ ] All 6 sections are present and filled in
- [ ] Category `README.md` table is updated
- [ ] `SEARCH.md` is updated with at least 2 entries
- [ ] The prompt has been tested in at least one AI assistant
- [ ] No secrets, personal data, or harmful content included

---

## Suggesting a New Category

If your prompt doesn't fit any existing category:
1. Open an issue with the title: `[New Category] your-category-name`
2. Describe what types of prompts belong there and include at least 3 example prompts that would go in it.
3. We'll review and create the category if there's enough demand.

---

## License

By contributing, you agree that your prompts are released under the [MIT License](./LICENSE) — free for anyone to use, remix, and share.
