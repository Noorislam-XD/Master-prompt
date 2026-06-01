# Governance

This document defines how the **Master Prompt Library** is maintained, how contributions are reviewed, and how decisions are made.

---

## Roles

### Maintainer
The repository maintainer (@Noorislam-XD) is responsible for:
- Final approval and merging of all pull requests
- Releasing new versions and updating the changelog
- Enforcing the [Code of Conduct](./CODE_OF_CONDUCT.md)
- Managing labels, milestones, and project direction

### Contributor
Anyone who opens an issue, submits a pull request, or participates in discussions. Contributors are expected to follow the [Code of Conduct](./CODE_OF_CONDUCT.md) and [Contributing Guide](./CONTRIBUTING.md).

### Reviewer (Community)
Experienced contributors who regularly provide high-quality feedback on pull requests. Anyone may comment and review — formal reviewer status is informal and based on participation.

---

## Decision Making

### Minor changes
Typo fixes, broken link repairs, formatting corrections, and small wording improvements may be merged by the maintainer without discussion.

### New prompts
New prompt files are reviewed against the [contribution checklist](./CONTRIBUTING.md). They require:
- A completed prompt submission (following the issue template or PR format)
- A valid source citation
- Confirmation that the prompt produces the described output
- No violation of the [prompt safety standards](./SECURITY.md#prompt-safety-standards)

Review target: **within 7 days** of submission.

### New categories
Adding a new top-level category (e.g., a new `/org` or domain folder) requires:
1. Opening an issue with the label `new-category` describing the proposed category, at least 3 planned prompts, and the rationale
2. A 3-day open comment period for community input
3. Maintainer approval before any files are merged

### Breaking changes
Changes that affect the structure of `prompts.json`, the frontmatter schema, or the folder layout are breaking changes. These require:
1. An issue opened and labeled `breaking-change`
2. At least 5 days for community comment
3. A migration note added to `CHANGELOG.md`

---

## Contribution Workflow

```
1. Fork the repo
2. Create a branch: feature/your-prompt-name or fix/description
3. Make your changes following CONTRIBUTING.md
4. Open a Pull Request with a clear description
5. Address any review feedback
6. Maintainer merges once approved
```

Pull requests that do not follow [CONTRIBUTING.md](./CONTRIBUTING.md) or fail the checklist will be closed with a comment explaining what needs to be fixed.

---

## Release Process

Releases follow [Semantic Versioning](https://semver.org/):

| Change type | Version bump | Example |
|-------------|-------------|---------|
| New prompts or categories | Minor | 1.4.0 → 1.5.0 |
| Bug fixes, edits, corrections | Patch | 1.5.0 → 1.5.1 |
| Breaking schema/structure changes | Major | 1.x.x → 2.0.0 |

**Release steps:**
1. Update `CHANGELOG.md` with all changes under the new version heading
2. Update the `version` field in `prompts.json`
3. Create a GitHub Release with the version tag and changelog excerpt

---

## Conflict Resolution

If a contributor disagrees with a maintainer decision:
1. Comment on the PR or issue explaining the disagreement respectfully
2. The maintainer will respond with their reasoning within 5 days
3. If unresolved, the maintainer's decision is final

---

## Amendments to This Document

Changes to this governance document follow the same process as breaking changes — an issue, a comment period, and maintainer approval.

---

*Last updated: June 2026*
