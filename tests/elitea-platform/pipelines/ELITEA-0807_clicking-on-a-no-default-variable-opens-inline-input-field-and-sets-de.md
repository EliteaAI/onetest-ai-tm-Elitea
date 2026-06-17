---
id: ELITEA-0807
title: "Clicking + on a no-default variable opens inline input field and sets default value"
priority: medium
type: functional
module: pipelines
status: ready
execution_type: manual
tags: [issue:2676, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#2676]
---
# ELITEA-0807: Clicking + on a no-default variable opens inline input field and sets default value

**Module:** Pipelines · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that clicking the + icon on a no-default variable expands it into an inline editable input field, and that entering a value and saving changes the icon from + to ≡.

**Coverage:**
- + icon click expands variable into inline editable field
- "Default value" placeholder shown in empty field
- Value entered inline is accepted
- Icon changes from + to ≡ after value is set

## Preconditions

- Logged in to {{base_url}} with a valid user account
- A Pipeline with at least one custom state variable that has no default value

## Test Data

- Variable without default: e.g. str_null (type: string)
- Value to enter: hello world

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Pipeline. Open the STATE panel in collapsed mode. Locate a variable with no default value (showing + icon). | Variable row shows + icon next to the type badge. |
| 2 | Click the + icon on the variable. | The variable row expands into an inline editable input field. The field shows "Default value" placeholder text. |
| 3 | Type `hello world` into the inline input field. | Text is accepted and visible in the input field. |
| 4 | Click outside the field or otherwise confirm the input. Observe the icon. | The icon next to the type badge changes from + to ≡, indicating a default value is now set. |
| 5 | Save the pipeline. Verify the variable still shows ≡ in collapsed state. | Pipeline saved. Variable shows ≡ icon in collapsed state. |

## Expected Final State

Pipeline saved. Variable shows ≡ icon in collapsed state.

## Pass/Fail Criteria

**Pass:**
- + click opens inline field; placeholder shown; value entered; icon changes to ≡ after value set; persists after save

**Fail:**
- + click does nothing; placeholder not shown; icon does not change after value entered
