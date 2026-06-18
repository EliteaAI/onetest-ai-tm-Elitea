---
id: ELITEA-0744
title: "Dropdown reopen and reload consistency for unread-focused list"
priority: medium
type: functional
module: notifications
status: ready
execution_type: manual
tags: [feat:notifications, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5119]
---
# ELITEA-0744: Dropdown reopen and reload consistency for unread-focused list

**Module:** Notifications · **Priority:** Medium · **Type:** Functional

**Objective:** Verify notifications dropdown behavior is stable after close/reopen and reload when read state changes.

**Coverage:**
- Session close/reopen behavior
- Unread-focused list presentation
- Persistence after page reload

## Preconditions

User is logged in
At least 2 unread notifications exist

## Test Data

Environment URL: {{base_url}}
Notification sample: minimum 2 unread items

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open dropdown and mark one unread notification as read | Row state updates to read in current session |
| 2 | Close and reopen dropdown | List behavior matches unread-focused design consistently |
| 3 | Mark remaining visible unread notifications as read | No unread rows remain in current view |
| 4 | Refresh page and reopen dropdown | Read state persists and items do not reappear as unread |

## Expected Final State

Read state persists and items do not reappear as unread

## Pass/Fail Criteria

**Pass:**
- Behavior is consistent across reopen and reload
- Read state persists correctly

**Fail:**
- Inconsistent list filtering between reopen/reload
- Read items reappear as unread
