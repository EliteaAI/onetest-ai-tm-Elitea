---
id: ELITEA-1104
title: "Jira – Descriptive Error Returned for Invalid issue_key in \"Add file to issue description\""
priority: medium
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:image-generation, integration:jira, feat:toolkits]
requirements: [3180]
---
# ELITEA-1104: Jira – Descriptive Error Returned for Invalid issue_key in "Add file to issue description"

**Module:** Toolkits Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that a descriptive error message is returned when an invalid issue_key is provided to the Jira 'Add file to issue description' tool.

## Preconditions

- ELITEA platform accessible
- Jira toolkit configured with 'Add file to issue description' tool enabled
- Artifact bucket contains a valid file at /my-bucket/test-file.png

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Invoke 'Add file to issue description' with a non-existent issue_key (e.g., INVALID-99999) and a valid filepath /my-bucket/test-file.png | Tool returns a descriptive error message indicating the issue was not found (e.g., 404); no crash or silent failure |

## Expected Final State

Tool returns a descriptive error message indicating the issue was not found (e.g., 404); no crash or silent failure

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
