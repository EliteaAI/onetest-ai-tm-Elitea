---
id: ELITEA-4631
title: "ELITEA-4631: Skill Run History Page Display and Restore Chat from History"
priority: critical
type: regression
module: skills
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:skills, run-history, chat-restore]
requirements: [EliteaAI/elitea_issues#6927]
---
# ELITEA-4631: Skill Run History Page Display and Restore Chat from History

**Module:** Skills · **Priority:** Critical · **Type:** Regression

**Objective:** Verify that the Skill Run History page displays correctly with all required columns and status icons, and users can successfully restore chats from run history to continue conversations.

**Coverage:**
- Run history table displays with proper columns
- Status icons render correctly (success, error, stopped)
- Date/time, version, and user information visible
- Context menu with Restore Chat option
- Restore chat recreates conversation context
- Restored chat is functional

## Preconditions

- User is logged into {{base_url}}
- User has created at least one skill (e.g., "uppercase-text-converter")
- Skill has previous run history with multiple executions
- Runs exist with different statuses (success, error, stopped)

## Test Data

| Field | Value |
|-------|-------|
| Skill name | uppercase-text-converter |
| Expected runs | At least 3 runs with mixed statuses |
| Expected columns | Status icon, Date/Time, Version, User, Actions |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Skills page | Skills list displays |
| 2 | Open skill "uppercase-text-converter" (or similar skill with history) | Skill details page loads |
| 3 | Click on "Run History" tab or "Usage" section | Run History page displays |
| 4 | Verify table columns present | Table shows: Status icon, Date/Time, Version, User, Actions (3-dot menu) |
| 5 | Verify status icons render correctly | Success runs show green checkmark, errors show red X, stopped runs show orange/yellow icon |
| 6 | Verify date/time displayed in readable format | Recent runs show relative time (e.g., "2 hours ago"), older runs show date |
| 7 | Verify version badge displayed for each run | Version identifier visible (e.g., "v1", "base") |
| 8 | Click 3-dot menu (⋮) on a successful run row | Context menu appears with options |
| 9 | Verify "Restore Chat" option is present | "Restore Chat" option visible in context menu |
| 10 | Click "Restore Chat" | Action initiates |
| 11 | Observe chat restoration | New chat opens OR existing chat restored with skill run context |
| 12 | Verify chat contains skill run history | Chat shows previous messages/context from that run |
| 13 | Send a new message in restored chat | Message sends successfully |
| 14 | Verify skill responds in restored chat | Skill executes and responds, continuing the conversation |

## Expected Final State

- Run History page displays complete execution history with proper formatting
- All status icons, dates, versions visible and correct
- Context menu provides Restore Chat functionality
- Restored chat is fully functional with historical context
- User can continue conversation from restored point

## Pass/Fail Criteria

**Pass:**
- Run History table renders with all required columns
- Status icons display correctly for all run states
- Context menu appears with Restore Chat option
- Chat restoration creates functional chat with context
- Restored chat allows continued interaction

**Fail:**
- Run History table missing columns or data
- Status icons don't render or show wrong states
- Restore Chat option missing or doesn't work
- Restored chat doesn't contain historical context
- Can't send messages in restored chat

## Notes

**Source functional tests:** ELITEA-4329, ELITEA-4330, ELITEA-4332
**Regression rationale:** Critical monitoring and recovery workflow; combines run history display with chat restoration capability.
**Selected checkpoints:** Table display, status visualization, context menu, chat restoration with full functionality.
