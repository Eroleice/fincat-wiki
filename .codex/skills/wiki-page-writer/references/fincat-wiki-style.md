# FinCat Wiki Style

This reference captures conventions observed in the repository and should be used together with the Wiki.js Markdown reference.

## Page Shape

A typical page has YAML front matter, then body Markdown:

```markdown
---
title: 页面标题
description: 页面摘要
published: true
date: 2026-06-29T02:30:00.000Z
tags: 
editor: markdown
dateCreated: 2026-06-29T02:30:00.000Z
---

# 第一部分
正文。
```

Use the repository's existing front matter field order. Keep `tags:` as a scalar line unless existing pages in the same area use another form.

## Voice

Default to clear, compact Chinese. The wiki mixes personal notes with professional explanations, so write like a careful practitioner:

- State assumptions and scope early.
- Prefer concrete operational guidance over vague commentary.
- Keep paragraphs short.
- Use examples for workflows, policies, formulas, and configuration.
- Avoid promotional wording and unsupported certainty.

## Sources

For source-backed pages, follow the existing policy pages:

- `规范/内容规范/AI辅助创作.md`
- `规范/内容规范/可靠来源.md`
- `规范/内容规范/列明来源.md`

Practical rules:

- Facts, laws, standards, thresholds, dates, prices, policies, and technical claims need sources.
- Prefer official, primary, academic, regulatory, self-regulatory, or clearly accountable sources.
- Use footnotes close to the assertion they support.
- Do not cite low-quality blogs, forums, anonymous pages, generated summaries, or content farms for important claims.
- Do not cite AI tools or AI-generated summaries as sources for factual claims.
- If a source is used for a third-party opinion, label it as opinion and do not use it as the factual basis for another conclusion.

Local citation examples:

```markdown
某项规则自特定日期施行。[^rule-source]

[^rule-source]: 发布机关. 文件名称. 条款编号. (发布日期)[引用日期].
```

```markdown
某研究给出了测算方法。[^paper-source]

[^paper-source]: 作者. 文献题名. 出版物名, 年份, 卷(期): 页码.
```

```markdown
官方页面列明了该配置项。[^web-source]

[^web-source]: 主要责任者. 题名: 其他题目信息[文献类型标识/文献载体标识]. 发表网站, (发布日期)[引用日期]. URL.
```

## AI-Assisted Work

FinCat Wiki uses strong disclosure for material AI participation. If AI substantially drafts, rewrites, summarizes, translates, organizes sources, generates tables/diagrams/code, or otherwise changes page substance, add or update a page-end disclosure section.

Use this template after human verification:

```markdown
# AI辅助说明

> 本页曾使用 AI 工具辅助创作或修订。
>
> - AI工具/模型：
> - 参与方式：
> - 人工核验：
> - 最后核验日期：
{.is-info}
```

Use this template before human verification is complete:

```markdown
# AI辅助说明

> 本页曾使用 AI 工具辅助创作或修订。
>
> - AI工具/模型：
> - 参与方式：
> - 人工核验：未完成
> - 最后核验日期：
{.is-warning}
```

Simple spelling checks or Markdown formatting fixes that do not change substantive content do not require disclosure. When uncertain, disclose. For high-risk content such as finance, securities, law, tax, accounting, medicine, child safety, policies, and regulations, record verification status and the last verification date.

## Page Creation

When creating a page:

1. Choose the path from the existing taxonomy, for example `证券/交易/A股/页面名.md`.
2. Create missing directories only when the target file path requires them.
3. Use a concise Chinese `title`.
4. Use `description` as a short search/display summary.
5. Add an opening section that establishes scope before detailed sections.
6. Include sources for non-obvious facts before considering the page complete.

A useful default outline:

```markdown
# 概述

简要说明主题、适用范围和核心结论。

# 背景

解释概念来源、制度背景或使用场景。

# 主要内容

按逻辑拆分为二级标题。

# 注意事项

列出边界、例外、风险或常见误区。
```

Do not force this outline when existing category pages use a stronger local pattern.

## Revisions

When revising:

- Preserve existing citations unless the supported statement is removed.
- Prefer adding a new dated/source-backed paragraph to silently overwriting a historically meaningful statement.
- When updating current facts, include the exact effective date, publication date, or query date.
- If a source conflicts with existing text, explain the conflict in the page or final response rather than smoothing it away.

## Images

The repository stores page images under `assets/image/page/`. Reuse existing assets when possible, and migrate legacy root-level image paths when encountered.

Use:

```markdown
![家庭组网拓扑.png](/assets/image/page/家庭组网拓扑.png)
![中国产业园区分类](/assets/image/page/中国产业园区分类.png =100%x)
```

Prefer descriptive alt text for new content. If the exact filename is meaningful to the page, it can be used as the alt text.

## Category Notes

- `规范/`: site policy, source rules, disclaimers, contact/join pages. Be formal and conservative.
- `证券/`: regulatory, tax, accounting, transaction, investment-banking, and business notes. Use primary law/regulatory/self-regulatory sources wherever possible.
- `金融/`: CFA and finance learning notes. Use structured explanations, formulas, examples, and definitions.
- `养殖/`: parenting/home/life knowledge. Be practical; medical or child-safety claims need extra caution and reliable sources.
- `代码/`: technical notes. Use commands and code fences with language identifiers.
- `数学/` and `物理/`: derivations and problem-solving pages. Keep notation consistent and explain assumptions.
- `沙盒/`: experimental pages. Keep experiments isolated and do not generalize their style to formal pages.

## Completion Checklist

- Page path matches taxonomy.
- Front matter is valid and preserved.
- The body starts with a clear heading.
- Sources are present for factual claims.
- Footnotes render and are defined once.
- Images use wiki-served paths.
- Tables and tabs have blank lines and class markers in the right place.
- AI-assisted pages include the required page-end disclosure.
- The edit scope matches the user request.
