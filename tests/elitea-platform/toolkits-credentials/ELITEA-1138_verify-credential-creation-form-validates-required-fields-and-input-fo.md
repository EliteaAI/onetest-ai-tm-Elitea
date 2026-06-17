---
id: ELITEA-1138
title: "Verify credential creation form validates required fields and input formats correctly"
priority: high
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:credentials]
requirements: []
---
# ELITEA-1138: Verify credential creation form validates required fields and input formats correctly

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** The credential creation form has validation issues: required fields may not show validation errors when left empty, invalid input formats may be accepted without warning, and error messages may be unclear or missing, leading to failed credential creation with confusing feedback.

## Preconditions

User is logged into Elitea platform
User has permission to create credentials
User has access to Credentials page

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Credentials page and click the Create/Add credential button | Credential creation form opens with all fields empty and a credential type selector visible |
| 2 | Without filling any fields, click the Save/Create button to submit the empty form | Form shows validation errors on all required fields (e.g., name, type, token/API key). Form is NOT submitted |
| 3 | Select a credential type (e.g., GitHub) and verify which fields become required | Type-specific required fields are displayed with clear required indicators (asterisk or similar) |
| 4 | Fill in the name field with an invalid format (e.g., single character, very long string >100 chars, or special characters only) | Validation error appears if name doesn't meet requirements (min/max length, allowed characters) |
| 5 | Fill in the name with a valid value but leave the token/API key field empty, then submit | Validation error shown specifically for the missing token/API key field. Form is not submitted |
| 6 | Fill in all required fields with valid values and click Save/Create | Credential is created successfully. User is redirected to credentials list or sees success confirmation |
| 7 | Attempt to create another credential with the exact same name as the one just created | System either prevents duplicate names with a validation error or handles duplicates gracefully (e.g., appends suffix) |
| 8 | Create a credential and then immediately edit it — verify all fields are pre-populated correctly | Edit form shows all previously entered values correctly. Sensitive fields (tokens) may be masked but editable |
| 9 | Clean up by deleting the test credentials created during this test | Test credentials are successfully deleted |

## Expected Final State

Test credentials are successfully deleted

## Pass/Fail Criteria

PASS: All required fields show validation errors when empty, invalid inputs are rejected with clear messages, and valid submissions succeed
FAIL: Empty required fields are accepted, invalid inputs pass validation, error messages are missing/unclear, or form submits with incomplete data
