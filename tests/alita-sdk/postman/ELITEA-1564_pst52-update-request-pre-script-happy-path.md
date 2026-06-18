---
id: ELITEA-1564
title: "PST52 - Update Request Pre-Script (Happy Path)"
priority: high
type: functional
module: postman
status: ready
execution_type: automated
tags: [update_request_pre_script, scripts, postman, smoke]
requirements: []
---
# ELITEA-1564: PST52 - Update Request Pre-Script (Happy Path)

**Module:** Postman · **Priority:** High · **Type:** Functional

**Objective:** Validates that the update_request_pre_script tool successfully updates the pre-request scripts of an existing request.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME, POSTMAN_COLLECTION_ID, and POSTMAN_REQUEST_PATH env vars are set
Write access to the target collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
POSTMAN_REQUEST_PATH: path to an existing request
Pre-request script: pm.environment.set(\"timestamp\", new Date().toISOString());

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke update_request_pre_script with POSTMAN_COLLECTION_ID, POSTMAN_REQUEST_PATH, and a JavaScript pre-request script | Tool accepts pre-request script parameters |
| 3 | Capture the tool response and verify script saved | Tool confirms pre-request script updated without error |
| 4 | Validate LLM confirms pre-request script applied to the request | LLM confirms pre-script saved on request |

## Expected Final State

LLM confirms pre-script saved on request

## Pass/Fail Criteria

update_request_pre_script sets pre-request script on the request
Script confirmed saved on request
No exception raised
