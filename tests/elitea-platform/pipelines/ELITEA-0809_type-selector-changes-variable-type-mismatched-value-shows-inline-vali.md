---
id: ELITEA-0809
title: "Type selector changes variable type; mismatched value shows inline validation error"
priority: medium
type: functional
module: pipelines
status: ready
execution_type: manual
tags: [issue:2676, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#2676]
---
# ELITEA-0809: Type selector changes variable type; mismatched value shows inline validation error

**Module:** Pipelines · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that clicking the type badge on a state variable opens the type selector dropdown with all available types, that changing the type updates the variable correctly, and that entering a value that does not match the selected type displays an inline validation error.

**Coverage:**
- Type badge click opens dropdown with String, Number, List, JSON options
- Selecting a different type changes the variable type (badge updates)
- Entering a value incompatible with the selected type displays a clear inline error message
- Entering a valid value for the type clears the error
- ≡ icon correctly reflects whether a valid default value is set after type change

## Preconditions

- Logged in to {{base_url}} with a valid user account
- A Pipeline with at least one custom state variable

## Test Data

- Variable: e.g. list (type badge: #)
- Invalid value for Number type: hello → expected error: "Invalid number format"
- Valid value for Number type: 42
- Type change targets: String, Number, List, Json

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Pipeline. Open the STATE panel. Locate any custom state variable. Click its type badge (e.g. Abc, #, {}, ≡). | A dropdown opens listing the available types: String, Number, List, Json. The current type has a checkmark. |
| 2 | Select a different type from the dropdown (e.g. change from String to Number). | The type badge updates to # (Number). The variable now expects a numeric value. |
| 3 | Expand the variable (click ≡ or +). Enter an invalid value for the Number type (e.g. hello). | An inline validation error is displayed in red below the variable (e.g. "Invalid number format"). |
| 4 | Clear the invalid value and enter a valid number (e.g. 42). | The inline error disappears. The value 42 is accepted. The ≡ icon is shown indicating a default is set. |
| 5 | Change the type back to String via the dropdown. | Type badge reverts to Abc. No error shown. |
| 6 | Save the pipeline. Reopen it and verify the variable type and value are correct. | Variable type and value persisted correctly after save and reload. |

## Expected Final State

Variable type and value persisted correctly after save and reload.

## Pass/Fail Criteria

**Pass:**
- Type dropdown opens with all 4 types; selected type badge updates; invalid value shows inline error; valid value clears error; type and value persist after save

**Fail:**
- Type badge not clickable; dropdown missing types; invalid value accepted without error; error does not clear on valid input
