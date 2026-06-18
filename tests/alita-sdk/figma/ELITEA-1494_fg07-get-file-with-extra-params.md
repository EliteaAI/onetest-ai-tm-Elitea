---
id: ELITEA-1494
title: "FG07 - Get File with Extra Params"
priority: medium
type: functional
module: figma
status: ready
execution_type: automated
tags: [extra-params, filtering, get_file, figma, file]
requirements: []
---
# ELITEA-1494: FG07 - Get File with Extra Params

**Module:** Figma · **Priority:** Medium · **Type:** Functional

**Objective:** Test get_file with extra_params for output filtering and limiting, verifying that additional parameters are passed to the Figma API and affect the response (e.g., depth limiting, specific fields).

## Preconditions

Figma toolkit is configured and authenticated
FIGMA_TOOLKIT_ID and FIGMA_FILE_KEY env vars are set
Extra params configured for depth limiting or field filtering

## Test Data

FIGMA_TOOLKIT_ID: configured Figma toolkit ID
FIGMA_FILE_KEY: valid Figma file key
extra_params: {"depth": 1} or {"output_limit": 50} to limit response size

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Figma toolkit with valid API token | Toolkit authenticated |
| 2 | Set FIGMA_FILE_KEY to a valid file key | Environment variable set |
| 3 | Invoke get_file tool with file_key and extra_params={"depth": 1} | API request includes depth parameter limiting recursion |
| 4 | Validate response is returned without error | Filtered file response received |
| 5 | Compare response structure/size against an unfiltered call to confirm extra_params had effect | Filtered response is smaller or differently structured than default |

## Expected Final State

Filtered response is smaller or differently structured than default

## Pass/Fail Criteria

Response returned with extra params applied
Output is filtered or limited compared to default call
Tool completes without error
Response size differs measurably from unfiltered call
