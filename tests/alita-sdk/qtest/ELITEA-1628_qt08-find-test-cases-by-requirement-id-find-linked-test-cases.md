---
id: ELITEA-1628
title: "QT08 - find_test_cases_by_requirement_id: Find Linked Test Cases"
priority: high
type: functional
module: qtest
status: ready
execution_type: automated
tags: [find_test_cases_by_requirement_id, requirements, happy-path, linking, qtest]
requirements: []
---
# ELITEA-1628: QT08 - find_test_cases_by_requirement_id: Find Linked Test Cases

**Module:** Qtest · **Priority:** High · **Type:** Functional

**Objective:** Verify the qTest find_test_cases_by_requirement_id tool finds test cases linked to a requirement. Tests retrieval of test cases associated with a specific requirement ID (forward relationship).

## Preconditions

qTest toolkit is configured and authenticated
QTEST_TOOLKIT_NAME and QTEST_PROJECT_ID env vars are set
Project has at least one requirement (fallback uses RQ-1)

## Test Data

QTEST_TOOLKIT_NAME: name of configured qTest toolkit
QTEST_PROJECT_ID: ID of existing qTest project
requirement search DQL: "Status = 'New' or Status = 'Active'"
Fallback requirement: RQ-1

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the qTest toolkit using QTEST_TOOLKIT_NAME and valid credentials | Toolkit initializes without error |
| 2 | Search for a requirement using search_entities_by_dql with object_type='requirements' and DQL filter; fall back to RQ-1 if search fails | A requirement ID is available for the test |
| 3 | Extract the requirement ID from search results | Requirement ID (RQ-xxx format) is extracted |
| 4 | Invoke find_test_cases_by_requirement_id with the requirement ID | Tool executes without crashing |
| 5 | Validate the response contains 'test case', 'linked', or 'requirement' keywords and no error indicators | Response shows linked test cases or empty list; valid response structure; no errors |

## Expected Final State

Response shows linked test cases or empty list; valid response structure; no errors

## Pass/Fail Criteria

Tool executes without errors
Response structure is valid
No error indicators (Invalid requirement, exception)
Handles empty linked test case list gracefully
