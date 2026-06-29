# Repository Agent Rules

This repository is the Git-synced Markdown storage for a Wiki.js personal wiki. Treat `.md` files as live wiki pages.

Use `.codex/workflows/wiki-content-workflows.md` to route wiki work. Keep the default stack small: `wiki-page-writer` for content drafting/revision, `wiki-source-reviewer` for source and factual-risk review, and `wiki-maintainer` for mechanical site health.

Use `.codex/skills/wiki-page-writer/SKILL.md` for tasks that create, rewrite, expand, translate, update, or format wiki content. The skill includes the Wiki.js Markdown syntax reference and FinCat Wiki writing conventions.

Use `.codex/skills/wiki-source-reviewer/SKILL.md` for citation audits, factual verification, high-risk content review, source-quality checks, and pages involving laws, finance, medicine, safety, policies, standards, dates, thresholds, or other time-sensitive claims.

Use `.codex/skills/wiki-maintainer/SKILL.md` for front matter, broken links, image paths, missing assets, footnote mechanics, table/tabset/admonition formatting, AI disclosure presence, and other mechanical Wiki.js rendering or repository hygiene tasks.

Always preserve Wiki.js YAML front matter unless the user explicitly asks to change metadata. Do not remove `editor: markdown`, do not change `dateCreated`, and do not introduce unsupported syntax such as Obsidian backlinks or MDX components.

For factual, legal, financial, medical, policy, standards, or technical claims, verify reliable sources and cite them with footnotes. Prefer local source-policy pages under `规范/内容规范/` when deciding citation quality.

Follow `规范/内容规范/AI辅助创作.md` when AI participates in wiki writing. AI output is not a reliable source; never invent citations, laws, cases, data, dates, or source metadata. For material AI drafting, rewriting, summarizing, translating, source organization, or generated tables/diagrams/code, add or update the page-end `AI辅助说明` disclosure.

Use site-root paths for internal links and assets, for example `/证券/交易/A股/过户费` and `/assets/image/page/example.png`. Never write local Windows paths into page Markdown.
