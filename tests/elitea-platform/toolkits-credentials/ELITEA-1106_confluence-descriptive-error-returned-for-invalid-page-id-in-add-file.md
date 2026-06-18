---
id: ELITEA-1106
title: "Confluence – Descriptive Error Returned for Invalid page_id in \"Add file to page\""
priority: medium
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [integration:confluence, feat:image-generation, feat:toolkits]
requirements: [3180]
---
# ELITEA-1106: Confluence – Descriptive Error Returned for Invalid page_id in "Add file to page"

**Module:** Toolkits Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that a descriptive error message is returned when an invalid page_id is provided to the Confluence 'Add file to page' tool.

## Preconditions

- ELITEA platform accessible
- Confluence toolkit configured with 'Add file to page' tool enabled
- Artifact bucket contains a valid file at /my-bucket/test-file.png

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Invoke 'Add file to page' with a non-existent page_id (e.g., 999999999) and a valid filepath /my-bucket/test-file.png | Tool returns a descriptive error message indicating the page was not found (e.g., 404); no crash or silent failure |

## Expected Final State

Tool returns a descriptive error message indicating the page was not found (e.g., 404); no crash or silent failure

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
