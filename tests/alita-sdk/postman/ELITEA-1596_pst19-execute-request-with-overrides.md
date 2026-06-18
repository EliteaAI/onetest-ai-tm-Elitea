---
id: ELITEA-1596
title: "PST19 - Execute Request with Overrides"
priority: high
type: functional
module: postman
status: ready
execution_type: automated
tags: [execute_request, execution, overrides, postman]
requirements: []
---
# ELITEA-1596: PST19 - Execute Request with Overrides

**Module:** Postman · **Priority:** High · **Type:** Functional

**Objective:** Validates that the execute_request tool properly handles variable overrides, allowing custom values to be passed at execution time.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME and POSTMAN_COLLECTION_ID env vars are set
Collection contains a request that uses collection or environment variables
POSTMAN_REQUEST_PATH env var set to a request using variables

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
POSTMAN_REQUEST_PATH: path to a request using variables
Override variables: {baseUrl: https://override.example.com}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke execute_request with POSTMAN_COLLECTION_ID, POSTMAN_REQUEST_PATH, and override_variables dict with custom values | Tool accepts parameters with variable overrides |
| 3 | Capture the tool response | Request was executed using the overridden variable values |
| 4 | Validate LLM confirms the override values were applied and request succeeded | LLM confirms variable override applied correctly |

## Expected Final State

LLM confirms variable override applied correctly

## Pass/Fail Criteria

execute_request with variable overrides uses the provided values
Response reflects the overridden variable values
No exception raised
