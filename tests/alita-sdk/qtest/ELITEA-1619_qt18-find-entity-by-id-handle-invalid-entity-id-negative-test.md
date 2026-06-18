---
id: ELITEA-1619
title: "QT18 - find_entity_by_id: Handle Invalid Entity ID (Negative Test)"
priority: medium
type: functional
module: qtest
status: ready
execution_type: automated
tags: [find_entity_by_id, error-handling, negative-test, invalid-id, qtest]
requirements: []
---
# ELITEA-1619: QT18 - find_entity_by_id: Handle Invalid Entity ID (Negative Test)

**Module:** Qtest · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the qTest find_entity_by_id tool properly handles invalid entity ID formats. Tests error handling for malformed or non-existent entity IDs that do not match expected TC/RQ/TR/DF prefixes.

## Preconditions

qTest toolkit is configured and authenticated
QTEST_TOOLKIT_NAME and QTEST_PROJECT_ID env vars are set
Entity ID 'INVALID-999999' does not match any valid qTest entity type prefix

## Test Data

QTEST_TOOLKIT_NAME: name of configured qTest toolkit
QTEST_PROJECT_ID: ID of existing qTest project
Invalid entity ID: INVALID-999999

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the qTest toolkit using QTEST_TOOLKIT_NAME and valid credentials | Toolkit initializes without error |
| 2 | Invoke find_entity_by_id with entity_id='INVALID-999999' | Tool executes without crashing |
| 3 | Capture the lookup result | Response received (error expected) |
| 4 | Validate the response DOES contain error indicators ('Invalid entity', 'not found', 'error', 'format', 'Expected prefix') and DOES NOT contain success indicators ('QTest Id', 'Name', 'Description', 'successfully') | Error message indicates invalid ID format or unrecognized prefix; no entity data returned |

## Expected Final State

Error message indicates invalid ID format or unrecognized prefix; no entity data returned

## Pass/Fail Criteria

Tool was called (executed)
Response contains error indicator (Invalid entity, not found, error, format, Expected prefix)
No entity data fields returned (QTest Id, Name, Description)
Tool did not crash
