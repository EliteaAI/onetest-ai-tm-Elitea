---
id: ELITEA-1617
title: "QT17 - find_entity_by_id: Universal Entity Lookup"
priority: high
type: functional
module: qtest
status: ready
execution_type: automated
tags: [find_entity_by_id, universal-lookup, happy-path, entity, qtest]
requirements: []
---
# ELITEA-1617: QT17 - find_entity_by_id: Universal Entity Lookup

**Module:** Qtest · **Priority:** High · **Type:** Functional

**Objective:** Verify the qTest find_entity_by_id tool finds any entity by its ID using automatic type detection. Tests universal lookup across different entity types (TC, RQ, TR, DF) by parsing the ID prefix.

## Preconditions

qTest toolkit is configured and authenticated
QTEST_TOOLKIT_NAME and QTEST_PROJECT_ID env vars are set
Write access to the qTest project

## Test Data

QTEST_TOOLKIT_NAME: name of configured qTest toolkit
QTEST_PROJECT_ID: ID of existing qTest project
Test case: Name='QT17 Entity Lookup Test {timestamp}', Type=Manual, Status=New, Priority=Medium, 1 step

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the qTest toolkit using QTEST_TOOLKIT_NAME and valid credentials | Toolkit initializes without error |
| 2 | Create a test case via create_test_cases with Name='QT17 Entity Lookup Test {timestamp}' and one test step | Test case created with TC- and qTest numeric ID |
| 3 | Extract the TC- identifier from create response | TC-xxx ID extracted |
| 4 | Invoke find_entity_by_id with entity_id=<TC-xxx> (the created test case ID) | Tool automatically detects entity type from TC- prefix and looks up the entity |
| 5 | Validate the response contains 'Id', 'QTest Id', and 'Name' fields confirming entity was found | Full entity details returned; no error indicators |
| 6 | Invoke delete_test_case with the qTest ID to clean up | Test case deleted successfully |

## Expected Final State

Test case deleted successfully

## Pass/Fail Criteria

Tool automatically detects entity type from prefix
Response contains Id, QTest Id, and Name
Not error indicators (not found, exception, Invalid entity)
Cleanup succeeds
