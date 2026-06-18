---
id: ELITEA-0743
title: "Notifications dropdown usability and visual consistency after state changes"
priority: medium
type: functional
module: notifications
status: ready
execution_type: manual
tags: [feat:notifications, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5119]
---
# ELITEA-0743: Notifications dropdown usability and visual consistency after state changes

**Module:** Notifications · **Priority:** Medium · **Type:** Functional

**Objective:** Verify notifications dropdown remains usable and visually stable during repeated read-state changes.

**Coverage:**
- Repeated read/unread row updates
- Control clickability and layout stability
- Reopen rendering stability

## Preconditions

User is logged in
At least 2 unread notifications exist

## Test Data

Environment URL: {{base_url}}
Notification sample: at least 2 unread rows

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Notifications dropdown | Dropdown renders with expected controls and layout |
| 2 | Perform repeated mark as read and mark as unread actions | No layout breakage and controls remain clickable |
| 3 | Close and reopen dropdown | Updated states persist and rendering remains stable |
| 4 | Interact with other controls in dropdown | No clipping overlap or broken interactions |

## Expected Final State

No clipping overlap or broken interactions

## Pass/Fail Criteria

**Pass:**
- No visual or interaction regressions
- Controls remain usable after repeated state toggles

**Fail:**
- Broken layout, non-clickable controls, clipping, or flicker
