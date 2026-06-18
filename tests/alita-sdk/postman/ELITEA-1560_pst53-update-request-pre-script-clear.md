---
id: ELITEA-1560
title: "PST53 - Update Request Pre-Script (Clear)"
priority: medium
type: functional
module: postman
status: ready
execution_type: automated
tags: [update_request_pre_script, edge-case, scripts, postman]
requirements: []
---
# ELITEA-1560: PST53 - Update Request Pre-Script (Clear)

**Module:** Postman · **Priority:** Medium · **Type:** Functional

**Objective:** Validates that the update_request_pre_script tool properly handles clearing pre-request scripts by setting them to empty string.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME, POSTMAN_COLLECTION_ID, and POSTMAN_REQUEST_PATH env vars are set
Request has an existing pre-request script
Write access to the target collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
POSTMAN_REQUEST_PATH: path to a request with an existing pre-request script
Script: (empty string)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke update_request_pre_script with POSTMAN_COLLECTION_ID, POSTMAN_REQUEST_PATH, and an empty string | Tool accepts empty script string |
| 3 | Capture the tool response | Tool confirms pre-request script cleared without error |
| 4 | Validate LLM confirms pre-request script removed from the request | LLM confirms pre-script cleared |

## Expected Final State

LLM confirms pre-script cleared

## Pass/Fail Criteria

update_request_pre_script with empty string clears the pre-request script
Request has no pre-request script after operation
No exception raised
