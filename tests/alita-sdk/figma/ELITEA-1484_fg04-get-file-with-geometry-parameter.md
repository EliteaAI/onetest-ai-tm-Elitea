---
id: ELITEA-1484
title: "FG04 - Get File with Geometry Parameter"
priority: medium
type: functional
module: figma
status: ready
execution_type: automated
tags: [geometry, get_file, vector, figma, file]
requirements: []
---
# ELITEA-1484: FG04 - Get File with Geometry Parameter

**Module:** Figma · **Priority:** Medium · **Type:** Functional

**Objective:** Test get_file with geometry parameter to export vector path data, verifying that geometry=paths causes vector data to be included in the response.

## Preconditions

Figma toolkit is configured and authenticated
FIGMA_TOOLKIT_ID and FIGMA_FILE_KEY env vars are set
Target file contains vector/path elements

## Test Data

FIGMA_TOOLKIT_ID: configured Figma toolkit ID
FIGMA_FILE_KEY: valid file key for a file containing vector/path elements
geometry parameter: "paths"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Figma toolkit with valid API token | Toolkit authenticated |
| 2 | Set FIGMA_FILE_KEY to a file containing vector/path elements | Environment variable set |
| 3 | Invoke get_file tool with file_key and geometry="paths" parameter | API request includes geometry query parameter |
| 4 | Validate response contains vector nodes with geometry data | Node objects include fillGeometry or strokeGeometry arrays |
| 5 | Compare to a call without geometry to confirm the parameter caused additional data | Geometry data present only in call with geometry parameter |

## Expected Final State

Geometry data present only in call with geometry parameter

## Pass/Fail Criteria

Response includes geometry vector data in node objects
fillGeometry or strokeGeometry arrays present in vector nodes
Response differs from call without geometry parameter
Tool completes without error
