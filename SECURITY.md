# Security Policy

## Scope

This repository contains **prompt templates** for use with large language models. It does not contain executable code deployed in production, user data, or authentication systems. However, we take security seriously in the following areas:

- Prompts that could be used to facilitate real-world harm
- Prompt injection techniques disguised as legitimate prompts
- Contributions containing malware, obfuscated scripts, or phishing content
- Privacy violations (e.g., prompts embedding real personal data)

---

## Supported Versions

| Version | Supported |
|---------|-----------|
| Latest (`main` branch) | ✅ Active |
| Older tagged releases | ⚠️ Best-effort |

---

## Reporting a Vulnerability

**Do not open a public GitHub issue for security vulnerabilities.**

If you discover a security concern — including a prompt that enables harmful outputs, a file containing malicious content, or a workflow vulnerability — please report it privately:

1. Go to the **[Security tab](https://github.com/Noorislam-XD/Master-prompt/security)** of this repository
2. Click **"Report a vulnerability"**
3. Describe the issue clearly, including:
   - Which file(s) are affected
   - What harm could result
   - Steps to reproduce (if applicable)

We will acknowledge your report within **48 hours** and aim to resolve confirmed issues within **7 days**.

---

## Responsible Disclosure Policy

We ask that you:

- Give us reasonable time to investigate and fix the issue before public disclosure
- Avoid accessing, modifying, or deleting data that does not belong to you
- Act in good faith

We commit to:

- Acknowledging your report promptly
- Keeping you informed of our progress
- Crediting you in the fix (if you wish) once resolved

---

## Prompt Safety Standards

All prompts in this library must meet the following safety standards:

- **No harmful instructions** — prompts must not facilitate violence, illegal activity, harassment, or deception
- **No jailbreaks** — prompts that attempt to bypass model safety features are not accepted
- **No PII** — prompts must not contain real personal information
- **Accurate attribution** — prompts must cite their actual source; plagiarism or false attribution is not permitted

Prompts that violate these standards will be removed and the contributor may be banned per the [Code of Conduct](./CODE_OF_CONDUCT.md).

---

## Dependencies

This repository has no runtime dependencies. If GitHub Actions workflows are added, they will be reviewed to ensure:

- No secrets are exposed in logs
- Third-party actions are pinned to specific commit SHAs
- Permissions follow the principle of least privilege

---

## Contact

For non-security questions, open a [GitHub Issue](https://github.com/Noorislam-XD/Master-prompt/issues).
For security issues, use the [private vulnerability report](https://github.com/Noorislam-XD/Master-prompt/security) channel.
