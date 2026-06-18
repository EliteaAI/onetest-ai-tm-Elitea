---
id: ELITEA-0941
title: "Viewer Role Has Read-Only Access and Can View Preview Mode"
priority: high
type: functional
module: project-context
status: ready
execution_type: manual
tags: [project-context, feat:settings, preview-mode, permissions, viewer-role, story:3395, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3395, EliteaAI/elitea_issues#5325]
---
# ELITEA-0941: Viewer Role Has Read-Only Access and Can View Preview Mode

**Module:** Project Context · **Priority:** High · **Type:** Functional

**Objective:** Verify that Viewer users have read-only access to Project Context and can open Preview mode to see rendered Markdown.

**Coverage:**
- Viewer cannot edit, upload, save, or toggle anything
- Viewer CAN open Preview mode and see rendered Markdown (not raw text)
- Applies to both Private and Team projects

## Preconditions

- Admin has saved Markdown content in Project Context: `# Hello
**Bold text**`
- Viewer account is a member of both a Private and Team project

## Test Data

- Markdown content to save: `# Hello
**Bold text**`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Admin saves the following Markdown in Project Context: '# Hello\n**Bold text**'. Log in as Viewer. Navigate to Private project → Settings → Project Context. | Page loads for Viewer. |
| 2 | Attempt to click in the editor field and type. | Field is not editable for Viewer. |
| 3 | Check for Save and Upload buttons. | No active Save or Upload button visible for Viewer. |
| 4 | Attempt to toggle the 'Enable Project Context' switch. | Toggle is disabled or not clickable for Viewer. |
| 5 | Check if a Preview mode button is visible. | Preview button is visible and clickable for Viewer. |
| 6 | Click Preview. | Content renders as formatted Markdown: 'Hello' appears as a heading, 'Bold text' appears bold. Raw Markdown syntax (# and **) is NOT shown. |
| 7 | Repeat steps 1–6 in a Team project. | Same read-only and preview behavior in Team project. |

## Expected Final State

Same read-only and preview behavior in Team project.

## Pass/Fail Criteria

**Pass:**
- All edit/save/upload/toggle controls absent or disabled for Viewer
- Preview button is visible and clickable
- Preview renders formatted Markdown (not raw text)

**Fail:**
- Viewer can modify or save content
- Preview button not accessible to Viewer
- Preview shows raw Markdown text instead of rendered output
