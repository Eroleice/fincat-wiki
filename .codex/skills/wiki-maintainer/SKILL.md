---
name: wiki-maintainer
description: Maintain Wiki.js-backed Markdown repositories by scanning and repairing page metadata, Wiki.js Markdown rendering hazards, internal links, image paths, footnotes, AI disclosure blocks, and repository hygiene. Use when Codex needs to audit or fix front matter, broken links, missing assets, root-level media, malformed tables, tabsets, admonitions, code fences, or other mechanical wiki issues.
---

# Wiki Maintainer

Use this skill for mechanical wiki maintenance. It keeps pages renderable and consistent, but does not decide whether factual claims are true. Use `wiki-source-reviewer` for evidence and source adequacy.

## Workflow

1. Check `git status --short` first and avoid overwriting unrelated user changes.
2. Identify the requested scope: one page, a directory, or the whole repository.
3. Run report-first for broad scans. Apply fixes directly only when the user asks for maintenance fixes or the scope is narrow and mechanical.
4. Preserve page content, YAML front matter meaning, and existing citations unless a mechanical fix requires moving or reformatting markup.
5. Re-run focused searches after fixes to confirm the issue is gone.

## Checks

Front matter:

- Starts at the first line and is closed by `---`.
- Keeps expected Wiki.js fields: `title`, `description`, `published`, `date`, `tags`, `editor`, `dateCreated`.
- Preserves `editor: markdown` and does not change `dateCreated`.

Markdown rendering:

- Tables have separator rows and surrounding blank lines.
- Fenced code blocks are closed and use useful language tags where possible.
- Footnote markers have definitions and definitions are not duplicated.
- Wiki.js blockquote classes such as `{.is-info}` and `{.is-warning}` sit after the intended block.
- Tabsets use parent headings with `{.tabset}` and child headings exactly one level deeper.

Links and assets:

- Internal wiki links use site-root paths such as `/证券/交易/A股/过户费`.
- Page images use `/assets/image/page/...` unless preserving a known legacy path is explicitly desired.
- Markdown never contains local Windows paths.
- Referenced local assets exist in the repository.

AI disclosure:

- Pages materially created or revised with AI include a page-end `# AI辅助说明`.
- Incomplete verification uses `{.is-warning}` and `人工核验：未完成`.
- Completed verification uses `{.is-info}` and records model/tool, participation mode, reviewer/status, and date.

## Report Format

For scans, return concise grouped results:

```markdown
## Front Matter
- file:line - Issue.

## Markdown Rendering
- file:line - Issue.

## Links And Assets
- file:line - Issue.

## AI Disclosure
- file:line - Issue.
```

If fixes were applied, summarize changed files and remaining issues. Do not claim source or factual verification; hand those to `wiki-source-reviewer`.
