---
id: ELITEA-1105
title: "QTest – Descriptive Error Returned for Invalid test_case_id in \"Add file to test case\""
priority: medium
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:image-generation, integration:qtest, feat:toolkits]
requirements: [3180]
---
# ELITEA-1105: QTest – Descriptive Error Returned for Invalid test_case_id in "Add file to test case"

**Module:** Toolkits Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that a descriptive error message is returned when an invalid test_case_id is provided to the QTest 'Add file to test case' tool.

## Preconditions

- ELITEA platform accessible
- QTest toolkit configured with 'Add file to test case' tool enabled
- Artifact bucket contains a valid file at /my-bucket/test-file.png

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Invoke 'Add file to test case' with a non-existent test_case_id (e.g., 999999999) and a valid filepath /my-bucket/test-file.png | Tool returns a descriptive error message indicating the test case was not found (e.g., 404); no crash or silent failure |

## Expected Final State

Tool returns a descriptive error message indicating the test case was not found (e.g., 404); no crash or silent failure

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
