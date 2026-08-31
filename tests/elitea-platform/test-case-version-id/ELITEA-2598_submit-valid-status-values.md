---
id: ELITEA-2598
title: "Submit Valid Status Values (Passed/Failed/Blocked/Incomplete/Unexecuted)"
priority: critical
type: functional
module: qtest-toolkit
status: ready
execution_type: manual
tags: [int:qtest, test-run, status, api-validation]
requirements: [EL-6336]
---
# ELITEA-2598: Submit Valid Status Values (Passed/Failed/Blocked/Incomplete/Unexecuted)

**Module:** QTest Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that all five valid QTest API status values can be submitted successfully without errors.

**Coverage:**
- All valid statuses accepted by API
- Each status updates correctly in QTest
- No API errors for valid values

## Preconditions

- Logged in to {{base_url}}
- QTest toolkit is configured and connected
- Multiple test runs available for testing (5 different runs recommended)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/{{project_id}}/toolkits` |
| Status Values to Test | Passed, Failed, Blocked, Incomplete, Unexecuted |
| Test Run IDs | 5 valid test run IDs from QTest |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to QTest toolkit and select "Update test run status" tool. | Tool configuration panel opens. |
| 2 | Enter Test Run ID #1 and select status "Passed". | Fields populated. |
| 3 | Execute the update. | Update succeeds; "Passed" status accepted. |
| 4 | Verify in QTest that Test Run #1 shows "Passed". | Status correctly reflected. |
| 5 | Enter Test Run ID #2 and select status "Failed". | Fields populated. |
| 6 | Execute the update. | Update succeeds; "Failed" status accepted. |
| 7 | Verify in QTest that Test Run #2 shows "Failed". | Status correctly reflected. |
| 8 | Enter Test Run ID #3 and select status "Blocked". | Fields populated. |
| 9 | Execute the update. | Update succeeds; "Blocked" status accepted. |
| 10 | Verify in QTest that Test Run #3 shows "Blocked". | Status correctly reflected. |
| 11 | Enter Test Run ID #4 and select status "Incomplete". | Fields populated. |
| 12 | Execute the update. | Update succeeds; "Incomplete" status accepted. |
| 13 | Verify in QTest that Test Run #4 shows "Incomplete". | Status correctly reflected. |
| 14 | Enter Test Run ID #5 and select status "Unexecuted". | Fields populated. |
| 15 | Execute the update. | Update succeeds; "Unexecuted" status accepted. |
| 16 | Verify in QTest that Test Run #5 shows "Unexecuted". | Status correctly reflected. |

## Expected Final State

All five valid status values are accepted by the QTest API and correctly reflected in QTest.

## Pass/Fail Criteria

**Pass:**
- All 5 status values (Passed, Failed, Blocked, Incomplete, Unexecuted) accepted
- Each update completes without errors
- QTest reflects correct status for each test run

**Fail:**
- Any valid status value rejected by API
- API error returned for valid status
- Status not correctly reflected in QTest
