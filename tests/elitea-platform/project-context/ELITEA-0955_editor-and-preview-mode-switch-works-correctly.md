---
id: ELITEA-0955
title: "Editor and Preview Mode Switch Works Correctly"
priority: critical
type: functional
module: project-context
status: ready
execution_type: manual
tags: [markdown-rendering, project-context, feat:settings, preview-mode, story:3395, issue:3395, r-2.0.4, xss]
requirements: [EliteaAI/elitea_issues#3395]
---
# ELITEA-0955: Editor and Preview Mode Switch Works Correctly

**Module:** Project Context · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the Editor ↔ Preview mode toggle switches correctly without a page reload and that each mode displays the appropriate view.

## Preconditions

- Project Context editor contains some Markdown content (e.g. `# Heading
**Bold**`)

## Test Data

- Markdown test payload: TC-PC-012-deep-markdown-structure.md
- XSS payload: TC-PC-006-xss-injection.md
- Admin or Editor user

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Project Context settings. Observe the current mode. | Editor mode is active by default. Raw Markdown text is editable. |
| 2 | Click the Preview button/tab. | Mode switches to Preview without a full page reload. Markdown is rendered as formatted content. |
| 3 | Click the Editor button/tab to switch back. | Mode returns to Editor. Raw Markdown is editable again. No content is lost. |
| 4 | Switch between Editor and Preview several times in a row. | Each switch is smooth and instant. No crashes, blank screens, or content corruption. |

## Expected Final State

Each switch is smooth and instant. No crashes, blank screens, or content corruption.

## Pass/Fail Criteria

**Pass:**
- Editor mode shows editable raw Markdown
- Preview mode shows rendered output
- Switching is instant, no page reload
- Content intact after repeated switching

**Fail:**
- Full page reload on switch
- Content lost after switching
- Blank or broken view after switch
