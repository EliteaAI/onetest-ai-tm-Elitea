---
id: ELITEA-2955
title: "Update Test Run With Valid Version ID"
priority: critical
type: functional
module: qtest-toolkit
status: ready
execution_type: manual
tags: [int:qtest, test-run, version-id, core-functionality]
requirements: [EL-6085]
---
# ELITEA-2955: Update Test Run With Valid Version ID

**Module:** QTest Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that updating a test run status with a valid testcase_version_id associates the result with that specific version in QTest.

**Coverage:**
- Version-specific test run updates work correctly
- Result is associated with correct version in QTest
- QTest displays result against the specified version

## Preconditions

- Logged in to {{base_url}}
- QTest toolkit is configured and connected
- Test run exists with multiple test case versions (e.g., 1.0, 2.0, 3.0)
- Valid numeric version ID is known (e.g., 101575054)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/{{project_id}}/toolkits` |
| QTest Toolkit | Pre-configured QTest toolkit |
| Test Run ID | Valid test run ID from QTest |
| Testcase Version ID | Valid numeric version ID (e.g., 101575054) |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits section. | Toolkits list displays. |
| 2 | Open the QTest toolkit. | QTest toolkit details page opens. |
| 3 | Select "Update test run status" tool. | Tool configuration panel opens. |
| 4 | Enter a valid Test Run ID. | Field accepts the value. |
| 5 | Enter a valid Testcase Version Id (numeric, e.g., 101575054). | Field accepts the numeric value. |
| 6 | Select status "Passed" from dropdown. | Status is selected. |
| 7 | Execute the update. | Request is sent to QTest API. |
| 8 | Verify the response indicates success. | No errors returned; success message shown. |
| 9 | Log into QTest and navigate to the test run. | Test run details page opens. |
| 10 | Verify the result is associated with the specified version. | Result shows against the correct version (e.g., version 1.0). |

## Expected Final State

Test run result is successfully associated with the specified test case version in QTest.

## Pass/Fail Criteria

**Pass:**
- Update succeeds with testcase_version_id
- Result correctly associated with specified version in QTest
- QTest shows result against the correct version number
- No errors during the update process

**Fail:**
- Update fails with valid version ID
- Result not associated with specified version
- Result appears against wrong version
- Error message returned despite valid data
