---
id: ELITEA-1111
title: "Confluence – Descriptive Error Returned for Invalid Filepath in \"Add file to page\""
priority: medium
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [integration:confluence, feat:image-generation, feat:toolkits]
requirements: [3180]
---
# ELITEA-1111: Confluence – Descriptive Error Returned for Invalid Filepath in "Add file to page"

**Module:** Toolkits Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that a descriptive error message is returned when an invalid Artifact filepath is provided to the Confluence 'Add file to page' tool.

## Preconditions

- ELITEA platform accessible
- Confluence toolkit configured with 'Add file to page' tool enabled
- A valid Confluence page ID is available

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Invoke 'Add file to page' with a valid page_id and a non-existent filepath (e.g., /nonexistent-bucket/no-such-file.png) | Tool returns a descriptive error message indicating the file was not found; no crash or silent failure |
| 2 | Invoke 'Add file to page' with a valid page_id and a malformed filepath (e.g., missing leading slash: my-bucket/file.png) | Tool returns a descriptive error message indicating the filepath format is invalid |

## Expected Final State

Tool returns a descriptive error message indicating the filepath format is invalid

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
