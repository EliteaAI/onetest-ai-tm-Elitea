---
id: ELITEA-1562
title: "PST55 - Duplicate Request (Special Characters)"
priority: medium
type: functional
module: postman
status: ready
execution_type: automated
tags: [duplicate_request, special-chars, edge-case, requests, postman]
requirements: []
---
# ELITEA-1562: PST55 - Duplicate Request (Special Characters)

**Module:** Postman · **Priority:** Medium · **Type:** Functional

**Objective:** Validates that the duplicate_request tool properly handles request names containing special characters and Unicode.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME, POSTMAN_COLLECTION_ID, and POSTMAN_REQUEST_PATH env vars are set
Write access to the target collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
POSTMAN_REQUEST_PATH: path to an existing request
New name: Auto Copy #1 (test) &amp; backup

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke duplicate_request with POSTMAN_COLLECTION_ID, POSTMAN_REQUEST_PATH, and a name containing special characters | Tool accepts special character name |
| 3 | Capture the tool response and verify new request created with expected name | Duplicated request name matches input including special chars |
| 4 | Delete the duplicated request to clean up | Cleanup successful |
| 5 | Validate LLM confirms name with special chars preserved on duplicate | LLM confirms special character name on duplicate request |

## Expected Final State

LLM confirms special character name on duplicate request

## Pass/Fail Criteria

duplicate_request with special characters in name preserves the name exactly
Duplicated request name matches special character input
No exception raised
