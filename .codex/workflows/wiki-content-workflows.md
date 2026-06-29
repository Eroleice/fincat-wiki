# Wiki Content Workflows

Use these workflows to route FinCat Wiki tasks without over-splitting agents. The default stack is one writer, one source reviewer, and one maintainer.

## Routing

| Task | Primary Skill | Secondary Check |
|:----|:----|:----|
| Create, rewrite, expand, translate, or format a page | `wiki-page-writer` | `wiki-source-reviewer` for high-risk facts |
| Audit citations, facts, dates, laws, policies, or medical/safety claims | `wiki-source-reviewer` | `wiki-maintainer` for footnote mechanics |
| Scan or repair front matter, links, images, footnotes, tabsets, tables, or AI disclosures | `wiki-maintainer` | `wiki-source-reviewer` if factual claims are touched |
| Broad high-risk page update | `wiki-page-writer` -> `wiki-source-reviewer` -> `wiki-maintainer` | Report unresolved verification gaps |

## Draft Or Revise

Use when the user asks to write or change page content.

1. Read `AGENTS.md`, `wiki-page-writer`, and the target page.
2. Read local content policies when facts, sources, or AI participation are involved.
3. Edit only the requested page scope.
4. Add or update `AI辅助说明` when AI materially participates.
5. For high-risk pages, run or recommend source review before considering the page done.

Done when the page has valid front matter, readable structure, Wiki.js-compatible Markdown, needed citations, and appropriate AI disclosure.

## Source Review

Use when correctness, sourcing, or high-risk claims matter.

1. Read the target page and local source/AI/disclaimer policies.
2. Inventory factual claims and map them to citations.
3. Classify unsupported, weakly supported, stale, or overbroad claims.
4. Return findings by severity, with file/line references where practical.
5. Only edit when asked; never invent replacement sources.

Done when each important claim is either supported, narrowed, flagged, or explicitly left as an unresolved verification gap.

## Content Review

Use when a page needs editorial judgment but not necessarily a rewrite.

1. Check whether the page scope, audience, and risk level are clear.
2. Identify overconfident language, missing caveats, missing applicability dates, and content that might be mistaken for specific advice.
3. For `证券/`, `金融/`, `养殖/医疗/`, `养殖/营养/`, and policy pages, prefer conservative wording and explicit source-backed scope.
4. Recommend changes first; apply them only when requested.

Done when the user can see what should change and why, without source review being conflated with style advice.

## Site Maintenance

Use for mechanical health across pages or directories.

1. Check worktree state and protect unrelated changes.
2. Scan the requested scope for front matter, Markdown rendering, links/assets, footnotes, and AI disclosure issues.
3. For broad scans, report first. For narrow mechanical requests, fix directly.
4. Re-run focused checks after fixes.

Done when mechanical issues are fixed or reported with exact next actions, and no content truth claims were silently changed.
