---
id: ELITEA-2954
title: "Update Test Run Without Version ID (Backward Compatibility)"
priority: critical
type: functional
module: qtest-toolkit
status: ready
execution_type: manual
tags: [int:qtest, test-run, version-id, backward-compatibility]
requirements: [EL-6085]
---
# ELITEA-2954: Update Test Run Without Version ID (Backward Compatibility)

**Module:** QTest Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that updating a test run status without providing testcase_version_id works as before (backward compatibility preserved).

**Coverage:**
- Existing calls without version ID continue to work
- No regression in core functionality
- Test run status updates successfully

## Preconditions

- Logged in to {{base_url}}
- QTest toolkit is configured and connected
- Test run exists in QTest project
- Agent or toolkit with QTest integration available

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/{{project_id}}/toolkits` |
| QTest Toolkit | Pre-configured QTest toolkit |
| Test Run ID | Valid test run ID from QTest |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits section. | Toolkits list displays. |
| 2 | Open the QTest toolkit. | QTest toolkit details page opens. |
| 3 | Select "Update test run status" tool. | Tool configuration panel opens. |
| 4 | Enter a valid Test Run ID. | Field accepts the value. |
| 5 | Select status "Passed" from dropdown. | Status is selected. |
| 6 | Leave Testcase Version Id field empty. | Field remains empty. |
| 7 | Execute the update. | Request is sent to QTest API. |
| 8 | Verify the response. | Update succeeds without errors. |
| 9 | Check the test run in QTest. | Status is updated to "Passed". |

## Expected Final State

Test run status is updated successfully in QTest without requiring a version ID, maintaining backward compatibility.

## Pass/Fail Criteria

**Pass:**
- Update succeeds without testcase_version_id
- No error messages returned
- Test run status reflects the update in QTest
- Existing behavior is preserved

**Fail:**
- Update fails when version ID is omitted
- Error message requires version ID
- Test run status not updated
- Regression in existing functionality
