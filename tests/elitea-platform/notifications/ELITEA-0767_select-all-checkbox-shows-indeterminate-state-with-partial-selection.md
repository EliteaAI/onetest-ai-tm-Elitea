---
id: ELITEA-0767
title: "Select All Checkbox Shows Indeterminate State with Partial Selection"
priority: medium
type: functional
module: notifications
status: draft
execution_type: manual
tags: [feat:notifications, story:4431, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4431]
---
# ELITEA-0767: Select All Checkbox Shows Indeterminate State with Partial Selection

**Module:** Notifications · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the Select All checkbox enters an indeterminate (partial/dash) state when some but not all rows on the page are selected.

**Coverage:**
- Indeterminate state appears when partial selection exists
- Clicking indeterminate state selects all rows
- Clicking the now fully-checked state deselects all rows

## Preconditions

- Logged in to {{base_url}}
- At least 3 notifications present on the page

## Test Data

- URL: {{base_url}}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to {{base_url}} | Notification Center table is displayed |
| 2 | Select some but not all row checkboxes (e.g., rows 1 and 2 out of 5) | Rows 1 and 2 are selected |
| 3 | Observe the Select All header checkbox | Select All shows an indeterminate visual state (dash/minus icon — neither fully checked nor empty) |
| 4 | Click the indeterminate Select All | All rows on the page become selected |
| 5 | Click the now-checked Select All | All rows are deselected |

## Expected Final State

All rows are deselected

## Pass/Fail Criteria

**Pass:**
- Indeterminate state is visually distinct from checked and unchecked
- Clicking indeterminate → all selected
- Clicking fully checked → all deselected

**Fail:**
- No indeterminate state shown with partial selection
- Clicking indeterminate does not select all rows
