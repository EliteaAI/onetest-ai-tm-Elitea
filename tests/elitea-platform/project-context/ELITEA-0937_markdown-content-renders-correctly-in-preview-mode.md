---
id: ELITEA-0937
title: "Markdown Content Renders Correctly in Preview Mode"
priority: medium
type: functional
module: project-context
status: ready
execution_type: manual
tags: [project-context, feat:settings, preview-mode, story:3395, markdown, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3395]
---
# ELITEA-0937: Markdown Content Renders Correctly in Preview Mode

**Module:** Project Context · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that all standard Markdown elements render correctly in Preview mode.

**Coverage:**
- Headings H1–H6, bullet/ordered lists, code blocks, tables, blockquotes
- Content inside code blocks is not parsed as Markdown

## Preconditions

- Logged in to ELITEA (`{{base_url}}`)

## Test Data

```
# H1
## H2
### H3
#### H4
##### H5
###### H6

- bullet item
1. ordered item

```python
# this should not be a heading
**not bold**


| Col A | Col B |
|---|---|
| 1 | 2 |

> blockquote text
```

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Set content containing all heading levels (# H1 through ###### H6), bullet list, numbered list, code block (```python), table, and blockquote (> text). Save. Switch to Preview. | H1–H6 render at correct sizes. Lists render correctly. Code block uses monospace font. Table renders with headers and rows. Blockquote is visually indented. |
| 2 | Inside a fenced code block, place: '# This is a heading' and '**this is bold**'. Switch to Preview. | Text inside the code block is rendered as plain text. The # and ** are shown literally, not parsed as Markdown. |

## Expected Final State

Text inside the code block is rendered as plain text. The # and ** are shown literally, not parsed as Markdown.

## Pass/Fail Criteria

**Pass:**
- All Markdown elements render visually in Preview
- Code block contents treated as plain text

**Fail:**
- Any Markdown element shows as raw syntax in Preview
- Code block content is parsed as Markdown
