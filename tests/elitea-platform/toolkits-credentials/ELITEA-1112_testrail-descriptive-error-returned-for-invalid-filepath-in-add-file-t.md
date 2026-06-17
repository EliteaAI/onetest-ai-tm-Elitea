---
id: ELITEA-1112
title: "TestRail – Descriptive Error Returned for Invalid Filepath in \"Add file to case\""
priority: medium
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:image-generation, integration:testrail, feat:toolkits]
requirements: [3180]
---
# ELITEA-1112: TestRail – Descriptive Error Returned for Invalid Filepath in "Add file to case"

**Module:** Toolkits Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that a descriptive error message is returned when an invalid Artifact filepath is provided to the TestRail 'Add file to case' tool.

## Preconditions

- ELITEA platform accessible
- TestRail toolkit configured with 'Add file to case' tool enabled
- A valid TestRail test case ID is available

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Invoke 'Add file to case' with a valid case_id and a non-existent filepath (e.g., /nonexistent-bucket/no-such-file.png) | Tool returns a descriptive error message indicating the file was not found; no crash or silent failure |
| 2 | Invoke 'Add file to case' with a valid case_id and a malformed filepath (e.g., missing leading slash: my-bucket/file.png) | Tool returns a descriptive error message indicating the filepath format is invalid |

## Expected Final State

Tool returns a descriptive error message indicating the filepath format is invalid

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
