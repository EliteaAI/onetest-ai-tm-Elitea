---
id: ELITEA-1204
title: "TC-014: Jira Toolkit Required Field Validation Still Works After Reorganization"
priority: high
type: functional
module: jira-toolkit-configuration
status: draft
execution_type: manual
tags: [feat:toolkits, issue:4029, int:jira, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#4029]
---
# ELITEA-1204: TC-014: Jira Toolkit Required Field Validation Still Works After Reorganization

**Module:** Jira Toolkit Configuration · **Priority:** High · **Type:** Functional

**Objective:** Verify that required field validation still works correctly in the Jira toolkit form after the UI reorganization. Attempting to save without required fields must trigger the appropriate validation messages.

Coverage:
- Required fields still validated on submit
- Correct error messages shown for missing required fields
- Form does not save with missing required fields

## Preconditions

- Logged in as User A
- Jira toolkit creation form open (empty)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Jira toolkit creation form, leave all fields empty | Form is open with no values entered |
| 2 | Attempt to save the toolkit without entering any values | Save is blocked; validation error messages appear on required fields (e.g., Toolkit Name, Jira URL, Token) |
| 3 | Fill in one required field but leave others empty; attempt to save again | Remaining empty required fields still show errors |
| 4 | Fill in all required fields with valid values and attempt to save | Form saves successfully; no validation errors remain |

## Expected Final State

Form saves successfully; no validation errors remain

## Pass/Fail Criteria

PASS:
- Submitting with empty required fields shows validation error messages
- Form is not saved until all required fields are filled

FAIL:
- Form submits successfully with required fields empty (validation bypassed)
- No error messages shown on submit with empty required fields
