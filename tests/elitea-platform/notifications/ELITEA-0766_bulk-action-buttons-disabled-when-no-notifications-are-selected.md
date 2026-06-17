---
id: ELITEA-0766
title: "Bulk Action Buttons Disabled When No Notifications Are Selected"
priority: medium
type: functional
module: notifications
status: draft
execution_type: manual
tags: [feat:notifications, story:4431, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4431]
---
# ELITEA-0766: Bulk Action Buttons Disabled When No Notifications Are Selected

**Module:** Notifications · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the bulk action buttons (Mark as read, Delete) are disabled or hidden when no checkboxes are selected, and activate only when at least one row is selected.

**Coverage:**
- Bulk action buttons absent/disabled by default (no selection)
- Buttons activate immediately when one checkbox is selected
- Buttons return to disabled/hidden state when selection is cleared

## Preconditions

- Logged in to {{base_url}}
- At least 2 notifications present

## Test Data

- URL: {{base_url}}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to {{base_url}} | Notification Center table is displayed with no rows selected |
| 2 | Verify no checkboxes are checked by default | All row checkboxes are in unchecked state |
| 3 | Verify the Mark as read and Delete buttons are absent or visually disabled/greyed out | Both bulk action buttons are disabled or not visible |
| 4 | Click the checkbox of one notification row | Row is selected |
| 5 | Verify both Mark as read and Delete buttons are now enabled and interactive | Both buttons are active and clickable |
| 6 | Deselect the checkbox by clicking it again | Row is deselected |
| 7 | Verify both buttons return to disabled or hidden state | Buttons are again disabled or absent |

## Expected Final State

Buttons are again disabled or absent

## Pass/Fail Criteria

**Pass:**
- Buttons are disabled/hidden with no selection
- Buttons activate on first selection
- Buttons deactivate when all selections are cleared

**Fail:**
- Buttons are always active regardless of selection
- Buttons remain disabled even after a row is selected
- Clicking an active button with no selection causes an error
