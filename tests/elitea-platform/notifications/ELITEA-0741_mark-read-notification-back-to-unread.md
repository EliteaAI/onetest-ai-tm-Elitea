---
id: ELITEA-0741
title: "Mark read notification back to unread"
priority: high
type: functional
module: notifications
status: ready
execution_type: manual
tags: [feat:notifications, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5119]
---
# ELITEA-0741: Mark read notification back to unread

**Module:** Notifications · **Priority:** High · **Type:** Functional

**Objective:** Verify read notification can be reverted to unread directly from dropdown.

**Coverage:**
- Mark as unread action
- Unread style restoration (bold)
- Action label toggle back to mark as read

## Preconditions

User is logged in
At least 1 notification is already in read state

## Test Data

Environment URL: {{base_url}}
Notification sample: at least 1 read row available in dropdown or list

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Notifications dropdown and locate a read notification | Target row is in read style and action is Mark as unread |
| 2 | Click Mark as unread on target row | Notification changes to unread immediately |
| 3 | Observe row visual style | Unread style returns (e.g., bold text appears) |
| 4 | Observe row action label | Action becomes Mark as read |

## Expected Final State

Action becomes Mark as read

## Pass/Fail Criteria

**Pass:**
- Revert to unread works in-place
- Unread style is restored
- Action label toggles correctly

**Fail:**
- Cannot revert or state update fails
- Styling is not restored
- Label/indicator mismatch
