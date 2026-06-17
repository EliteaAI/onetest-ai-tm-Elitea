---
id: ELITEA-0757
title: "Row Checkboxes Individual Selection and Deselection"
priority: medium
type: functional
module: notifications
status: draft
execution_type: manual
tags: [feat:notifications, story:4431, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4431]
---
# ELITEA-0757: Row Checkboxes Individual Selection and Deselection

**Module:** Notifications · **Priority:** Medium · **Type:** Functional

**Objective:** Verify each notification row has a checkbox that correctly toggles selected/deselected state, and that multi-row selection works.

**Coverage:**
- Each row displays a checkbox
- Clicking a checkbox selects the row with visual highlight
- Clicking again deselects the row
- Multiple non-consecutive rows can be selected simultaneously

## Preconditions

- Logged in to {{base_url}}
- At least 5 notifications present

## Test Data

- URL: {{base_url}}
- Rows to select: row 1 (individual toggle), rows 1+3+5 (multi-select)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to https://next.elitea.ai/app/notification-center | Notification Center table is displayed |
| 2 | Verify each notification row has a checkbox on the left side | All rows display a checkbox |
| 3 | Click the checkbox of the first row | Row receives a selected visual state (highlight or filled checkbox) and bulk actions bar activates |
| 4 | Click the same checkbox again | Row returns to unselected/default state |
| 5 | Click checkboxes for rows 1, 3, and 5 (non-consecutive) | All three selected rows are visually highlighted simultaneously |

## Expected Final State

All three selected rows are visually highlighted simultaneously

## Pass/Fail Criteria

**Pass:**
- All rows display checkboxes
- Selected rows are visually distinct from unselected ones
- Multiple non-consecutive rows can be selected simultaneously

**Fail:**
- Checkboxes are absent from rows
- Clicking checkbox does not change row state
- Only consecutive rows can be selected
