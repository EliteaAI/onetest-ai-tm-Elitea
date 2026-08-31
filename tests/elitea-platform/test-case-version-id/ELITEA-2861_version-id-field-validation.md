---
id: ELITEA-2861
title: "Version ID Field Validation"
priority: high
type: ui-validation
module: qtest-toolkit
status: ready
execution_type: manual
tags: [int:qtest, test-run, version-id, field-validation, ui]
requirements: [EL-6340]
---
# ELITEA-2861: Version ID Field Validation

**Module:** QTest Toolkit · **Priority:** High · **Type:** UI Validation

**Objective:** Verify that the Testcase Version Id field properly validates input and provides clear guidance on expected format.

**Coverage:**
- Field accepts numeric version IDs
- Field validation for invalid input
- Tooltip explains expected format
- Field length validation

## Preconditions

- Logged in to {{base_url}}
- QTest toolkit is configured

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/{{project_id}}/toolkits` |
| Valid Version ID | 101575054 (numeric) |
| Invalid Inputs | "4.0" (decimal), "version1" (text), "1.0" (decimal) |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to QTest toolkit and select "Update test run status" tool. | Tool configuration panel opens. |
| 2 | Locate the Testcase Version Id field. | Field is visible and optional. |
| 3 | Click on the information tooltip for Testcase Version Id. | Tooltip displays. |
| 4 | Verify tooltip explains field expects numeric ID. | Tooltip mentions "numeric version ID". |
| 5 | Verify tooltip instructs to use Get Test Case Versions tool. | Reference to lookup tool included. |
| 6 | Attempt to enter decimal value "4.0". | Either: (a) "." character rejected, or (b) field type supports decimals. |
| 7 | Attempt to enter text value "version1". | Non-numeric input rejected or flagged. |
| 8 | Enter valid numeric ID "101575054". | Field accepts the value. |
| 9 | Attempt to enter very long number (20+ digits). | Field has max length validation (rejects or truncates). |
| 10 | Clear the field and leave it empty. | Empty value accepted (field is optional). |

## Expected Final State

Testcase Version Id field validates input appropriately and provides clear guidance on expected format.

## Pass/Fail Criteria

**Pass:**
- Field accepts valid numeric IDs
- Tooltip clearly explains expected format
- Tooltip references Get Test Case Versions tool for lookup
- Field has reasonable max length (10-15 characters)
- Invalid input handled gracefully (rejected or clear error)

**Fail:**
- Field accepts any input without validation
- No guidance on expected format
- No max length validation (accepts unlimited input)
- Confusing error messages for invalid input
