---
name: wiki-source-reviewer
description: Review Wiki.js-backed Markdown wiki pages for source reliability, footnote quality, factual support, AI-source misuse, and high-risk content risk. Use when Codex needs to audit citations, verify source adequacy, classify unsupported claims, check legal/financial/medical/policy assertions, or produce a source-review report before or after page edits.
---

# Wiki Source Reviewer

Use this skill when the task is about whether a wiki page is well-supported, up to date, properly cited, or safe to publish. Review evidence and risk; do not polish prose unless the user explicitly asks for fixes.

## Core Workflow

1. Read the target page completely, including YAML front matter, footnotes, and any `AI辅助说明`.
2. Read local policy pages when present: `规范/内容规范/可靠来源.md`, `规范/内容规范/列明来源.md`, `规范/内容规范/AI辅助创作.md`, and `规范/声明/免责声明.md`.
3. Build a claim inventory for verifiable statements: numbers, dates, prices, thresholds, laws, regulations, standards, policies, cases, medical/safety claims, technical instructions, and strong recommendations.
4. Match each claim to nearby citations. Check whether the cited source directly supports the exact statement, not merely the general topic.
5. Classify source quality using local rules. Prefer official, primary, academic, regulatory, self-regulatory, or clearly accountable sources. Treat AI tools, anonymous pages, generated summaries, content farms, forums, and uncited claims as unsupported.
6. For high-risk pages, check whether the page states scope, effective dates, update dates, exceptions, and reader-risk warnings where needed.
7. Report findings first, ordered by severity. Include file/line references where practical.

## Severity

- `P0`: likely false, fabricated, dangerous, legally/medically/financially risky, or cites a nonexistent source.
- `P1`: important claim lacks source, source does not support the claim, or source is stale for a time-sensitive rule.
- `P2`: citation metadata is incomplete, source quality is weak, or claim needs narrower wording.
- `P3`: style or maintainability issue in footnotes, citation placement, or source formatting.

## Output

For review-only tasks, return:

```markdown
## Findings
- [P1] file:line - Issue summary. Evidence and suggested action.

## Source Gaps
- Claim needing source or verification.

## Notes
- Residual risk, unavailable sources, or assumptions.
```

If no issues are found, say so clearly and mention residual verification limits.

## Fixing Rules

Only edit pages when the user asks for fixes. Preserve Wiki.js front matter and page structure. Do not invent missing citations, titles, dates, file numbers, laws, or URLs.

When fixing:

- Add sources only after verifying the original source.
- Replace unsupported certainty with narrower language if no source is available.
- Mark unresolved high-risk material as needing verification instead of pretending it is verified.
- Update or add `AI辅助说明` if AI materially changes page substance.
