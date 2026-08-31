---
id: ELITEA-2858
title: "Invalid Version ID Returns Descriptive Error"
priority: critical
type: negative
module: qtest-toolkit
status: ready
execution_type: manual
tags: [int:qtest, test-run, version-id, error-handling]
requirements: [EL-6085]
---
# ELITEA-2858: Invalid Version ID Returns Descriptive Error

**Module:** QTest Toolkit · **Priority:** Critical · **Type:** Negative

**Objective:** Verify that providing an invalid or non-existent testcase_version_id returns a descriptive error message with valid alternatives.

**Coverage:**
- Error handling for invalid version IDs
- Error message includes valid version alternatives
- No partial updates occur on error

## Preconditions

- Logged in to {{base_url}}
- QTest toolkit is configured and connected
- Test run exists in QTest
- Test case has known valid versions

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/{{project_id}}/toolkits` |
| QTest Toolkit | Pre-configured QTest toolkit |
| Test Run ID | Valid test run ID from QTest |
| Invalid Version ID | Non-existent ID (e.g., 999999999) |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits section. | Toolkits list displays. |
| 2 | Open the QTest toolkit. | QTest toolkit details page opens. |
| 3 | Select "Update test run status" tool. | Tool configuration panel opens. |
| 4 | Enter a valid Test Run ID. | Field accepts the value. |
| 5 | Enter an invalid/non-existent Testcase Version Id (e.g., 999999999). | Field accepts the value. |
| 6 | Select status "Passed" from dropdown. | Status is selected. |
| 7 | Execute the update. | Request is sent to QTest API. |
| 8 | Observe the error response. | Descriptive error message is returned. |
| 9 | Verify error message content. | Error includes list of valid version IDs for the test case. |
| 10 | Verify error message format. | Shows format like "101575054 (1.0), 101575055 (2.0), etc." |
| 11 | Check QTest to verify no partial update occurred. | Test run status unchanged. |

## Expected Final State

A clear, actionable error message is displayed with valid version ID alternatives, and no partial update occurs.

## Pass/Fail Criteria

**Pass:**
- Descriptive error message returned
- Error includes list of valid version IDs
- Valid version names shown alongside IDs (e.g., "101575054 (1.0)")
- No partial update to test run
- User can identify correct version ID from error

**Fail:**
- Generic or unclear error message
- No valid alternatives provided
- Partial update occurs despite error
- Silent failure with no feedback
