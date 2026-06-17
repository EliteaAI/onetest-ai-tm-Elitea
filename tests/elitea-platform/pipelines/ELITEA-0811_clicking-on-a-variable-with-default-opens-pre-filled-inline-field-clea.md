---
id: ELITEA-0811
title: "Clicking ≡ on a variable with default opens pre-filled inline field; clearing reverts to +"
priority: medium
type: functional
module: pipelines
status: ready
execution_type: manual
tags: [issue:2676, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#2676]
---
# ELITEA-0811: Clicking ≡ on a variable with default opens pre-filled inline field; clearing reverts to +

**Module:** Pipelines · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that clicking the ≡ icon on a variable with a default value expands it into an inline input field showing the existing value, that the value can be edited, and that clearing it reverts the icon to +.

**Coverage:**
- ≡ click expands variable showing existing value in inline field
- Value can be modified inline
- Clearing the value reverts icon from ≡ to +

## Preconditions

- Logged in to {{base_url}} with a valid user account
- A Pipeline with at least one custom state variable that has a default value set

## Test Data

- Variable with default: e.g. number = 911
- New value: 42

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Pipeline. Open the STATE panel. Locate a variable with a default value (showing ≡ icon). | Variable row shows ≡ icon next to type badge. |
| 2 | Click the ≡ icon on the variable. | Variable row expands into an inline editable input field pre-filled with the existing default value (e.g. 911). |
| 3 | Clear the existing value and type `42`. Confirm/click outside. | Value updates to 42. Icon remains ≡. |
| 4 | Click ≡ again to expand. Clear the value entirely. Confirm/click outside. | Input field is empty (shows "Default value" placeholder). Icon changes from ≡ to +. |
| 5 | Save the pipeline. Verify the variable shows + in collapsed state. | Pipeline saved. Variable shows + icon — no default value. |

## Expected Final State

Pipeline saved. Variable shows + icon — no default value.

## Pass/Fail Criteria

**Pass:**
- ≡ opens pre-filled field; value editable; clearing reverts icon to +; persists after save

**Fail:**
- Field opens empty instead of pre-filled; clearing does not revert icon
