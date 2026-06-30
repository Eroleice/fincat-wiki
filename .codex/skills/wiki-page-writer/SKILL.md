---
name: wiki-page-writer
description: Write, revise, and update Wiki.js-backed Markdown wiki pages in a Git-synced content repository such as FinCat Wiki. Use when Codex needs to create or edit .md wiki pages, preserve Wiki.js front matter, apply Wiki.js-compatible Markdown syntax, add images/tables/tabs/admonitions/diagrams/footnotes, maintain source citations, or adapt content to the local Chinese personal-wiki style.
---

# Wiki Page Writer

Use this skill for writing work inside a Wiki.js Git storage repository. Treat the Markdown files as live wiki pages, not generic notes.

## Workflow

1. Identify the target page path. If the user gives a Wiki path, map it to the matching `.md` file; if the file is absent, create it under the corresponding directory.
2. Read the whole target page before editing. For any AI-assisted wiki writing or revision, read `规范/内容规范/AI辅助创作.md` if present. For factual, legal, financial, medical, technical, or policy content, also read the local source rules if present: `规范/内容规范/可靠来源.md` and `规范/内容规范/列明来源.md`.
3. Preserve the YAML front matter block and its field order unless creating a new page. Do not remove `editor: markdown`.
4. Make scoped content edits. Keep the page's existing voice, heading depth, link style, image path style, and citation style unless the user asks for a rewrite.
5. Verify Markdown rendering hazards before finishing: blank lines around tables/code/admonitions, matched footnote IDs, valid image paths, no accidental Windows paths, no unsupported Obsidian/MDX syntax.
6. When facts may be current or consequential, verify with reliable sources and cite them in footnotes. Prefer official, primary, or authoritative sources.
7. If AI materially drafts, rewrites, summarizes, translates, organizes sources, generates diagrams/tables/code, or otherwise changes page substance, add or update the page-end `AI辅助说明` required by the local AI policy.
8. After completing the full document-editing workflow and verification, commit the current task's changes directly. Check `git status --short`, stage only files changed for the current task, and use a concise commit message.

## Front Matter

Existing pages use this Wiki.js export shape:

```yaml
---
title: 页面标题
description: 简短描述
published: true
date: 2026-06-29T02:30:00.000Z
tags: 
editor: markdown
dateCreated: 2026-06-29T02:30:00.000Z
---
```

For new pages, set `title`, `description`, `published: true`, `editor: markdown`, and UTC ISO timestamps with milliseconds. Leave `tags:` blank if no useful tag is known; otherwise follow the repository's existing scalar tag style.

When editing existing pages, update `date` only if the task changes page content and the repository convention/user request expects metadata updates. Do not change `dateCreated`.

## Wiki.js Markdown

Use CommonMark and GitHub Flavored Markdown as the baseline. Wiki.js also supports footnotes, content tabs, Wiki.js blockquote/list/table classes, image dimensions, Mermaid, PlantUML, keyboard keys, subscript/superscript, and decorate syntax.

Read `references/wiki-js-markdown.md` when using non-basic Markdown, adding media, tables, tabs, admonitions, diagrams, or validating renderer compatibility.

## Local Style

Write in concise Chinese by default. Favor explanatory headings, short paragraphs, and sourced assertions over encyclopedic sprawl. Use footnotes for references when the page makes verifiable claims.

Read `references/fincat-wiki-style.md` when creating a page, revising citations, organizing a topic, adding images/assets, or deciding how to phrase source-backed content.

## Images And Assets

When inserting or moving page images, store local image files under `assets/image/page/` and reference them with site-root Markdown paths such as `/assets/image/page/example.png`. Do not add new page images at the repository root.

## AI-Assisted Disclosure

AI output is never a reliable source. Do not cite AI tools for factual claims and do not publish AI-supplied citations until each source is verified from the original material.

When the local page `规范/内容规范/AI辅助创作.md` exists, follow its strong disclosure rule. Use a page-end `# AI辅助说明` section for material AI participation. Use `{.is-info}` when human verification is complete, and `{.is-warning}` with `人工核验：未完成` when verification is incomplete.

## Editing Guardrails

- Do not replace the whole page when a focused patch is enough.
- Do not reorder large sections merely for polish.
- Do not invent citations, source titles, laws, standards, numbers, or dates.
- Do not treat AI-generated text, summaries, or source suggestions as evidence.
- Do not use raw HTML unless Wiki.js Markdown has no clean equivalent; `<kbd>` is acceptable.
- Do not use `[[wiki links]]`, MDX components, front matter arrays, or app-specific syntax unless an existing local page proves it renders correctly.
- Use site-root paths for wiki links and media, for example `/养殖/装修/家庭组网` and `/assets/image/page/example.png`, not local filesystem paths.
