---
id: ELITEA-1467
title: "CF15 - Execute Generic Confluence (GET Request)"
priority: critical
type: functional
module: confluence
status: ready
execution_type: automated
tags: [execute_generic_confluence, get-request, confluence, smoke, api]
requirements: []
---
# ELITEA-1467: CF15 - Execute Generic Confluence (GET Request)

**Module:** Confluence · **Priority:** Critical · **Type:** Functional

**Objective:** Verify execute_generic_confluence tool executes a generic Confluence REST API GET request and returns formatted response string as "HTTP: {method}{url} -> {status_code}{reason}{response_text}".

## Preconditions

Confluence toolkit is configured and authenticated
CF_TOOLKIT_ID env var is set
Valid Confluence REST API GET endpoint available

## Test Data

CF_TOOLKIT_ID: Confluence toolkit ID
HTTP method: GET
API endpoint: '/rest/api/space' (or similar valid GET endpoint)
Expected response format: 'HTTP: GET{url} -> 200 OK {response_text}'

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call execute_generic_confluence tool with method='GET' and a valid Confluence REST API endpoint (e.g., '/rest/api/space' to list spaces) | Tool executes successfully, returns formatted HTTP response string |
| 2 | LLM validates: response is formatted as 'HTTP: {method}{url} -> {status_code}{reason}{response_text}', status code is 2xx, response contains data | Validation confirms execute_generic_confluence correctly executes GET request and returns properly formatted response |

## Expected Final State

Validation confirms execute_generic_confluence correctly executes GET request and returns properly formatted response

## Pass/Fail Criteria

PASS: Response formatted as "HTTP: {method}{url} -> {status_code}{reason}{response_text}", status code is 2xx
FAIL: Tool crashes, malformed response format, non-2xx status
