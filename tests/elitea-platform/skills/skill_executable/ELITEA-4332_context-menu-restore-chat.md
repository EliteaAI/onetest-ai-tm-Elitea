---
id: ELITEA-4332
title: "Verify context menu 'Restore chat' action restores conversation in Run panel"
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
- Run panel is accessible

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills/all/[skillId]/history` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Skill Run History page | Run History table displays |
| 2 | Click the three-dot menu icon on any run entry | Context menu opens |
| 3 | Verify "Restore chat" option is visible | "Restore chat" option appears |
| 4 | Click "Restore chat" | Run panel opens with the conversation |
| 5 | Verify all messages from the run are loaded | Complete conversation thread displays |
| 6 | Check that the panel shows the correct run metadata | Timestamp, version, and duration match |
| 7 | Verify the conversation is in the expected state (read-only or editable) | State matches system design (same as direct click) |

## Expected Final State

The conversation from the selected run is fully restored in the Run panel via the context menu action.

## Pass/Fail Criteria

**Pass:**
- "Restore chat" option works from context menu
- Run panel opens with complete conversation
- Metadata is accurate
- Behavior matches direct click restoration

**Fail:**
- "Restore chat" option is missing or disabled
- Run panel does not open or shows wrong content
- Conversation is incomplete
- Metadata mismatch or error occurs
