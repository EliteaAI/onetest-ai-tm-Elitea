---
id: ELITEA-1568
title: "PST49 - Update Request Auth (Basic)"
priority: medium
type: functional
module: postman
status: ready
execution_type: automated
tags: [update_request_auth, basic-auth, requests, postman]
requirements: []
---
# ELITEA-1568: PST49 - Update Request Auth (Basic)

**Module:** Postman · **Priority:** Medium · **Type:** Functional

**Objective:** Validates that the update_request_auth tool properly handles different authentication types including basic authentication.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME, POSTMAN_COLLECTION_ID, and POSTMAN_REQUEST_PATH env vars are set
Write access to the target collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
POSTMAN_REQUEST_PATH: path to an existing request
Auth type: basic
Username: testuser
Password: testpass

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke update_request_auth with POSTMAN_COLLECTION_ID, POSTMAN_REQUEST_PATH, auth_type=basic, username, and password | Tool accepts basic auth parameters |
| 3 | Capture the tool response and verify auth type set | Tool confirms auth set to basic type with credentials |
| 4 | Validate LLM confirms basic auth applied to the request | LLM confirms basic auth credentials saved on request |

## Expected Final State

LLM confirms basic auth credentials saved on request

## Pass/Fail Criteria

update_request_auth with basic auth sets username and password
Auth type confirmed as basic with correct credentials
No exception raised
