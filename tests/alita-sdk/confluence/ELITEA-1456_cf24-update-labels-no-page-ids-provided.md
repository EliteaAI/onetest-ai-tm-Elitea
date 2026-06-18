---
id: ELITEA-1456
title: "CF24 - Update Labels (No Page IDs Provided)"
priority: high
type: functional
module: confluence
status: ready
execution_type: automated
tags: [error-handling, update_labels, confluence, negative, labels]
requirements: []
---
# ELITEA-1456: CF24 - Update Labels (No Page IDs Provided)

**Module:** Confluence · **Priority:** High · **Type:** Functional

**Objective:** Verify update_labels tool handles missing page IDs gracefully (empty list or None), returning an error message stating "Either list of page_ids should be provided" without crashing.

## Preconditions

Confluence toolkit is configured and authenticated
CF_TOOLKIT_ID env var is set
NEGATIVE test — page_ids parameter is empty list or None

## Test Data

CF_TOOLKIT_ID: Confluence toolkit ID
page_ids: [] (empty list) or None
Labels: ['test-label'] (valid labels provided, only page_ids is missing)
Expected error message: contains 'Either list of page_ids should be provided'

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call update_labels tool with an empty list or None for page_ids parameter and the labels to add | Tool executes without crashing, returns appropriate validation error |
| 2 | LLM validates: response contains message stating 'Either list of page_ids should be provided', error is informative, no unhandled exceptions | Validation confirms update_labels handles missing/empty page_ids gracefully with correct validation message |

## Expected Final State

Validation confirms update_labels handles missing/empty page_ids gracefully with correct validation message

## Pass/Fail Criteria

PASS: Error message states "Either list of page_ids should be provided", no crash
FAIL: Tool throws unhandled exception, returns wrong error message, or unexpectedly succeeds with empty list
