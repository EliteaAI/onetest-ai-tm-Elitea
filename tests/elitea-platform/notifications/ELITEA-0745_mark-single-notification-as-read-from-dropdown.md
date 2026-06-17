---
id: ELITEA-0745
title: "Mark single notification as read from dropdown"
priority: high
type: functional
module: notifications
status: ready
execution_type: manual
tags: [feat:notifications, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5119]
---
# ELITEA-0745: Mark single notification as read from dropdown

**Module:** Notifications · **Priority:** High · **Type:** Functional

**Objective:** Verify unread notification can be marked as read directly from dropdown.

**Coverage:**
- In-place mark as read
- Read visual style (bold removed)
- Action label switch to mark as unread

## Preconditions

User is logged in
At least 1 unread notification exists

## Test Data

Environment URL: {{base_url}}
User role: standard user with notifications access
Notification sample: at least 1 unread row

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Notifications dropdown | Unread notifications are visible with unread styling |
| 2 | On one unread row click Mark as read | Notification changes to read state immediately |
| 3 | Observe same row style | Unread emphasis is removed (e.g., bold text removed) |
| 4 | Observe same row action label | Action label changes to Mark as unread |

## Expected Final State

Action label changes to Mark as unread

## Pass/Fail Criteria

**Pass:**
- Read state is applied immediately
- Bold/unread styling is removed
- Action label becomes Mark as unread

**Fail:**
- State does not change immediately
- Styling remains unread after action
- Action label does not switch
