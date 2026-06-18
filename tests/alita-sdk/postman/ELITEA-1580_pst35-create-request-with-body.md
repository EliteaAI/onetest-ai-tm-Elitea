---
id: ELITEA-1580
title: "PST35 - Create Request with Body"
priority: medium
type: functional
module: postman
status: ready
execution_type: automated
tags: [create_request, requests, postman, headers, body]
requirements: []
---
# ELITEA-1580: PST35 - Create Request with Body

**Module:** Postman · **Priority:** Medium · **Type:** Functional

**Objective:** Validates that the create_request tool successfully creates a POST request with request body and headers.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME and POSTMAN_COLLECTION_ID env vars are set
POSTMAN_FOLDER_PATH set to an existing folder
Write access to the target collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
POSTMAN_FOLDER_PATH: path to an existing folder
Request name: Auto POST Request
Method: POST
URL: https://httpbin.org/post
Body: {\"key\": \"value\", \"test\": true}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke create_request with method=POST, URL, and a JSON body payload | Tool accepts POST request parameters including body |
| 3 | Capture the tool response and verify request created with body | Response confirms request created with body content preserved |
| 4 | Delete the created request to clean up | Cleanup successful |
| 5 | Validate LLM confirms POST request with body created successfully | LLM confirms request body preserved in created request |

## Expected Final State

LLM confirms request body preserved in created request

## Pass/Fail Criteria

create_request with POST method and JSON body creates request with body preserved
Request body type and content confirmed
No exception raised
