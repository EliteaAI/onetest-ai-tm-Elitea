---
id: ELITEA-2316
title: "Open MDX File Generated in Chat"
priority: critical
type: functional
module: chat
status: draft
execution_type: manual
tags: [feat:chat, feat:artifacts, feat:canvas, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5846]
---
# ELITEA-2316: Open MDX File Generated in Chat

**Module:** Chat · **Priority:** Critical · **Type:** Functional

**Objective:** Verify MDX files generated via Artifacts toolkit in chat can be opened and previewed

## Preconditions

- User is logged into NEXT environment
- Chat interface is accessible
- Artifacts toolkit is available

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Chat interface | Chat page loads |
| 2 | Send message: "Create an MDX file with a heading and paragraph" | AI processes request |
| 3 | Wait for AI to generate MDX file using Artifacts toolkit | File created |
| 4 | Observe chat response shows artifact/file item | File item appears |
| 5 | Note file name has .mdx extension | Extension is .mdx |
| 6 | Click on the file item or "View/Edit" action | Canvas opens |
| 7 | Verify file opens in Preview mode | Preview mode active |

## Expected Results

- MDX file is successfully generated via chat
- File appears in chat response as clickable artifact
- File name displays correctly with .mdx extension
- "View/Edit file" or Preview action is visible
- Clicking the action opens Canvas
- Canvas opens in Preview mode by default
- Can switch to Raw mode from chat-generated file
- Link to Artifacts bucket and file path is preserved
- File is accessible from Artifacts section

## Pass/Fail Criteria

**Pass:**
- Chat successfully generates MDX file
- File opens from chat in Canvas Preview mode
- All MDX features work as expected

**Fail:**
- File generation fails
- Cannot open file from chat
- File doesn't open in Canvas
- Preview mode not available
