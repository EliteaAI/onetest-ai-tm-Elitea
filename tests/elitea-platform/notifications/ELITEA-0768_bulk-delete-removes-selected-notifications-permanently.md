---
id: ELITEA-0768
title: "Bulk Delete Removes Selected Notifications Permanently"
priority: medium
type: functional
module: notifications
status: draft
execution_type: manual
tags: [feat:notifications, story:4431, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4431]
---
# ELITEA-0768: Bulk Delete Removes Selected Notifications Permanently

**Module:** Notifications · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that selecting one or more notifications and clicking Delete permanently removes those notifications from the table.

**Coverage:**
- Single notification deletion via checkbox + Delete bulk action
- Multi-notification deletion (3 simultaneously)
- Remaining notifications are intact after deletion

## Preconditions

- Logged in to {{base_url}}
- At least 3 notifications present in the Notification Center

## Test Data

- URL: {{base_url}}
- Select rows: row 1 (single delete test), rows 1+2+3 (bulk delete test)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to {{base_url}} | Notification Center table is displayed |
| 2 | Click the checkbox of the first row | Row is selected, bulk actions area activates |
| 3 | Click the Delete bulk action button. If a confirmation dialog appears, confirm it. | Deletion is triggered |
| 4 | Verify the selected notification is no longer in the table | Deleted notification is removed from the list |
| 5 | Verify all other notifications remain intact | Remaining notifications are unchanged |
| 6 | Select 3 notifications simultaneously using their checkboxes | All 3 rows are selected |
| 7 | Click Delete and confirm if prompted | Deletion is triggered for all 3 |
| 8 | Verify all 3 selected notifications are removed from the table | All 3 are gone from the list |
| 9 | Verify remaining notifications are unaffected | No unintended deletions occurred |

## Expected Final State

No unintended deletions occurred

## Pass/Fail Criteria

**Pass:**
- Both single and bulk deletions succeed
- Deleted notifications do not reappear on refresh
- Unselected notifications remain in the table

**Fail:**
- Delete button is not available after selection
- Deleted notifications still appear after action
- Unintended notifications are removed
