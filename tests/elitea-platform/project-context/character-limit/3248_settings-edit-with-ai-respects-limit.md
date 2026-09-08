---
id: "3248"
title: "Settings: Edit with AI respects 2500-character limit"
priority: critical
type: functional
module: project-context
status: draft
execution_type: manual
tags: [feat:project-setup, story:6344, r-2.0.6, project-context-builder, edit-with-ai, character-limit]
requirements: [EliteaAI/elitea_issues#6344]
---

# 3248: Settings: Edit with AI respects 2500-character limit

## Preconditions

- User has Editor or Admin role
- Project Context exists with some content (e.g., 1500 characters)
- Project Context toggle is enabled

## Test Data

| Field | Value |
|-------|-------|
| Existing content | ~1500 characters of project context |
| Edit request | "Expand this context with more details about integrations and security" |
| Character limit | 2500 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → Project Context | Page loads with existing content |
| 2 | Click "Edit" to enter edit mode | Edit mode activated |
| 3 | Click "Edit with AI" button | AI editing interface opens |
| 4 | Provide instructions to expand/modify the content | AI processes the edit request |
| 5 | Wait for AI-edited content to appear | Edited content is displayed |
| 6 | Verify the edited content length | Content is ≤2500 characters |

## Expected Final State

AI-edited project context content does not exceed 2500 characters, even when asked to expand existing content.

## Pass/Fail Criteria

**Pass:**
- Edited content ≤2500 characters
- Edits are meaningful and coherent
- Original intent is preserved while respecting limit

**Fail:**
- Edited content exceeds 2500 characters
- Content is truncated mid-edit
- AI ignores the limit when expanding content
