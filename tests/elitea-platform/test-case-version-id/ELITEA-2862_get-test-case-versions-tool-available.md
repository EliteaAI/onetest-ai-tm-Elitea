---
id: ELITEA-2862
title: "Get Test Case Versions Tool Available and Functional"
priority: high
type: functional
module: qtest-toolkit
status: ready
execution_type: manual
tags: [int:qtest, test-case-versions, tool-availability]
requirements: [EL-6085]
---
# ELITEA-2862: Get Test Case Versions Tool Available and Functional

**Module:** QTest Toolkit · **Priority:** High · **Type:** Functional

**Objective:** Verify that the "Get Test Case Versions" tool is available in QTest toolkit and returns version metadata correctly.

**Coverage:**
- Tool availability in QTest toolkit
- Tool accepts testcase_id as input
- Tool returns version ID and version name for all versions
- Works for test cases with single or multiple versions

## Preconditions

- Logged in to {{base_url}}
- QTest toolkit is configured and connected
- Test case exists in QTest with multiple versions (e.g., 1.0, 2.0, 3.0)
- Test case with single version also available

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/{{project_id}}/toolkits` |
| Multi-version Test Case ID | Test case ID with versions 1.0, 2.0, 3.0 |
| Single-version Test Case ID | Test case ID with only version 1.0 |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits section. | Toolkits list displays. |
| 2 | Open the QTest toolkit. | QTest toolkit details page opens. |
| 3 | Look for "Get Test Case Versions" tool in Read tools section. | Tool is visible and available. |
| 4 | Select "Get Test Case Versions" tool. | Tool configuration panel opens. |
| 5 | Verify testcase_id is a required parameter. | Field is marked as required. |
| 6 | Enter a test case ID with multiple versions. | Field accepts the value. |
| 7 | Execute the tool. | Tool runs successfully. |
| 8 | Verify response includes all versions. | Response shows all versions (e.g., 1.0, 2.0, 3.0). |
| 9 | Verify each version has ID and name. | Format: {id: 101575054, name: "1.0"}, etc. |
| 10 | Enter a test case ID with single version. | Field accepts the value. |
| 11 | Execute the tool. | Tool runs successfully. |
| 12 | Verify response shows single version correctly. | One version returned with ID and name. |

## Expected Final State

Get Test Case Versions tool is available and returns accurate version metadata for both single and multi-version test cases.

## Pass/Fail Criteria

**Pass:**
- Tool is available in QTest toolkit
- Tool accepts testcase_id parameter
- Returns version ID and version name for all versions
- Works correctly for multi-version test cases
- Works correctly for single-version test cases
- Response format is clear and usable

**Fail:**
- Tool not available in toolkit
- Tool does not accept testcase_id
- Missing version ID or name in response
- Incorrect versions returned
- Tool fails for single-version test cases
