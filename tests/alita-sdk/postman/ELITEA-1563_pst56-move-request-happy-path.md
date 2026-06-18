---
id: ELITEA-1563
title: "PST56 - Move Request (Happy Path)"
priority: high
type: functional
module: postman
status: ready
execution_type: automated
tags: [move_request, requests, postman, smoke]
requirements: []
---
# ELITEA-1563: PST56 - Move Request (Happy Path)

**Module:** Postman · **Priority:** High · **Type:** Functional

**Objective:** Validates that the move_request tool successfully moves a request to a different folder within the collection.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME, POSTMAN_COLLECTION_ID, and POSTMAN_REQUEST_PATH env vars are set
A target folder exists in the collection
Write access to the target collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
POSTMAN_REQUEST_PATH: path to an existing request in a folder
Target folder path: AnotherFolder

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke move_request with POSTMAN_COLLECTION_ID, POSTMAN_REQUEST_PATH, and a target folder path | Tool accepts move parameters |
| 3 | Capture the tool response and verify request moved | Tool confirms request moved to new folder |
| 4 | Validate LLM confirms request appears at new path | LLM confirms move operation succeeded |

## Expected Final State

LLM confirms move operation succeeded

## Pass/Fail Criteria

move_request relocates request to target folder
Request appears in new folder after move
No exception raised
