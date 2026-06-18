---
id: ELITEA-1107
title: "TestRail – Descriptive Error Returned for Invalid case_id in \"Add file to case\""
priority: medium
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:image-generation, integration:testrail, feat:toolkits]
requirements: [3180]
---
# ELITEA-1107: TestRail – Descriptive Error Returned for Invalid case_id in "Add file to case"

**Module:** Toolkits Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that a descriptive error message is returned when an invalid case_id is provided to the TestRail 'Add file to case' tool.

## Preconditions

- ELITEA platform accessible
- TestRail toolkit configured with 'Add file to case' tool enabled
- Artifact bucket contains a valid file at /my-bucket/test-file.png

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Invoke 'Add file to case' with a non-existent case_id (e.g., 999999999) and a valid filepath /my-bucket/test-file.png | Tool returns a descriptive error message indicating the test case was not found (e.g., 404); no crash or silent failure |

## Expected Final State

Tool returns a descriptive error message indicating the test case was not found (e.g., 404); no crash or silent failure

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
