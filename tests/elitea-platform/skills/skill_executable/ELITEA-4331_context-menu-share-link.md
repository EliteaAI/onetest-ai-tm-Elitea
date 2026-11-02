---
id: ELITEA-4331
title: "Verify context menu 'Share link' action generates and copies shareable URL"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6927]
---

## Preconditions

- User is logged in to `{{base_url}}`
- At least one skill run exists in history
- User has permission to share skill runs

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills/all/[skillId]/history` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Skill Run History page | Run History table displays |
| 2 | Click the three-dot menu icon on any run entry | Context menu opens with options |
| 3 | Verify "Share link" option is visible | "Share link" option appears in the menu |
| 4 | Click "Share link" | System generates a shareable URL |
| 5 | Check for visual feedback (toast/notification) | Success message or notification displays |
| 6 | Paste the copied link from clipboard | Link is successfully copied |
| 7 | Open the shared link in a new browser tab/window | Run loads correctly from the shared URL |
| 8 | Verify the loaded run matches the original | Content and metadata are identical |

## Expected Final State

A shareable link is generated, copied to clipboard, and successfully opens the specific run when accessed.

## Pass/Fail Criteria

**Pass:**
- "Share link" option is available in context menu
- Link is generated and copied to clipboard
- Visual feedback confirms the action
- Shared link opens the correct run

**Fail:**
- "Share link" option is missing or disabled
- Link is not copied to clipboard
- No visual feedback provided
- Shared link does not work or loads incorrect run
