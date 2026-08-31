---
id: ELITEA-2859
title: "Status Tooltip Shows Only Valid API Statuses"
priority: critical
type: ui-validation
module: qtest-toolkit
status: ready
execution_type: manual
tags: [int:qtest, test-run, status, tooltip, ui]
requirements: [EL-6336]
---
# ELITEA-2859: Status Tooltip Shows Only Valid API Statuses

**Module:** QTest Toolkit · **Priority:** Critical · **Type:** UI Validation

**Objective:** Verify that the Status field tooltip in QTest toolkit displays only the valid QTest API statuses and does not include rejected values.

**Coverage:**
- Status tooltip accuracy
- Valid statuses listed: Blocked, Failed, Incomplete, Passed, Unexecuted
- Invalid statuses NOT shown: Skipped, Broken, No Result, Pending, Unknown

## Preconditions

- Logged in to {{base_url}}
- QTest toolkit is configured

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/{{project_id}}/toolkits` |
| Valid Statuses | Blocked, Failed, Incomplete, Passed, Unexecuted |
| Invalid Statuses | Skipped, Broken, No Result, Pending, Unknown |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits section. | Toolkits list displays. |
| 2 | Open the QTest toolkit. | QTest toolkit details page opens. |
| 3 | Select "Update test run status" tool. | Tool configuration panel opens. |
| 4 | Locate the Status field. | Status field is visible. |
| 5 | Click on the information tooltip icon for Status field. | Tooltip popup displays. |
| 6 | Verify tooltip contains "Passed". | "Passed" is listed. |
| 7 | Verify tooltip contains "Failed". | "Failed" is listed. |
| 8 | Verify tooltip contains "Blocked". | "Blocked" is listed. |
| 9 | Verify tooltip contains "Incomplete". | "Incomplete" is listed. |
| 10 | Verify tooltip contains "Unexecuted". | "Unexecuted" is listed. |
| 11 | Verify tooltip does NOT contain "Skipped". | "Skipped" is NOT listed. |
| 12 | Verify tooltip does NOT contain "Broken". | "Broken" is NOT listed. |
| 13 | Verify tooltip does NOT contain "No Result". | "No Result" is NOT listed. |
| 14 | Verify tooltip does NOT contain "Pending". | "Pending" is NOT listed. |
| 15 | Verify tooltip does NOT contain "Unknown". | "Unknown" is NOT listed. |

## Expected Final State

Status tooltip displays only the 5 valid QTest API statuses without any invalid or rejected status values.

## Pass/Fail Criteria

**Pass:**
- All 5 valid statuses listed: Blocked, Failed, Incomplete, Passed, Unexecuted
- None of the invalid statuses shown: Skipped, Broken, No Result, Pending, Unknown
- Tooltip is clear and readable

**Fail:**
- Any invalid status (Skipped, Broken, etc.) appears in tooltip
- Any valid status is missing from tooltip
- Tooltip shows outdated or incorrect information
