---
id: ELITEA-1623
title: "QT10 - link_tests_to_qtest_requirement: Link Test Cases to Requirement"
priority: high
type: functional
module: qtest
status: ready
execution_type: automated
tags: [link_tests_to_qtest_requirement, requirements, happy-path, linking, qtest]
requirements: []
---
# ELITEA-1623: QT10 - link_tests_to_qtest_requirement: Link Test Cases to Requirement

**Module:** Qtest · **Priority:** High · **Type:** Functional

**Objective:** Verify the qTest link_tests_to_qtest_requirement tool links multiple test cases to a qTest requirement. Tests creating two test cases and linking them to an internal requirement ID.

## Preconditions

qTest toolkit is configured and authenticated
QTEST_TOOLKIT_NAME, QTEST_PROJECT_ID, and QTEST_REQUIREMENT_ID env vars are set
Write access to the qTest project
A valid requirement (default: RQ-1) exists in the project

## Test Data

QTEST_TOOLKIT_NAME: name of configured qTest toolkit
QTEST_PROJECT_ID: ID of existing qTest project
QTEST_REQUIREMENT_ID: RQ-1 (or env override)
Test case 1: Name='QT10 Link Test 1 {timestamp}', 1 step
Test case 2: Name='QT10 Link Test 2 {timestamp}', 1 step

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the qTest toolkit using QTEST_TOOLKIT_NAME and valid credentials | Toolkit initializes without error |
| 2 | Create two test cases via create_test_cases: 'QT10 Link Test 1 {timestamp}' and 'QT10 Link Test 2 {timestamp}' | Both test cases created with TC- identifiers |
| 3 | Extract both TC- identifiers from the create responses | Two TC-xxx IDs extracted |
| 4 | Invoke link_tests_to_qtest_requirement with the two TC- IDs and requirement_id=QTEST_REQUIREMENT_ID | Tool executes and returns response |
| 5 | Validate the response contains 'linked', 'successfully', 'added', or 'associated' | Linkage confirmed; no error indicators |
| 6 | Invoke delete_test_case for both created test cases to clean up | Both test cases deleted successfully |

## Expected Final State

Both test cases deleted successfully

## Pass/Fail Criteria

Tool executes without errors
Response contains 'linked', 'successfully', 'added', or 'associated'
No error indicators (Unable to link, exception)
Both cleanup deletions succeed
