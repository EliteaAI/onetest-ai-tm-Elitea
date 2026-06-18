---
id: ELITEA-1496
title: "FG01 - Get File Nodes (Happy Path)"
priority: high
type: functional
module: figma
status: ready
execution_type: automated
tags: [get_file_nodes, nodes, smoke, figma]
requirements: []
---
# ELITEA-1496: FG01 - Get File Nodes (Happy Path)

**Module:** Figma · **Priority:** High · **Type:** Functional

**Objective:** Verify get_file_nodes retrieves specific nodes from a Figma file using known node IDs, returning node data with properties.

## Preconditions

Figma toolkit is configured and authenticated
FIGMA_TOOLKIT_ID, FIGMA_FILE_KEY, and FIGMA_NODE_IDS env vars are set
Target Figma file is accessible with valid node IDs

## Test Data

FIGMA_TOOLKIT_ID: configured Figma toolkit ID
FIGMA_FILE_KEY: valid Figma file key (e.g., "abcXYZ123abc")
FIGMA_NODE_IDS: comma-separated list of valid node IDs in the file (e.g., "1:2,3:4")

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Figma toolkit with valid API token and set FIGMA_TOOLKIT_ID | Toolkit is configured and authenticated successfully |
| 2 | Set FIGMA_FILE_KEY to a valid file key and FIGMA_NODE_IDS to known valid node IDs (e.g., "1:2,3:4") | Environment variables are set |
| 3 | Invoke get_file_nodes tool with file_key and node_ids parameters | Tool executes and API request is made |
| 4 | Validate response contains a nodes map with entries for each requested node ID | Nodes map returned with all requested node IDs as keys |
| 5 | Verify each node object contains type, name, and document properties | Node data is complete and properly structured |
| 6 | Confirm no error messages in the response | Response is clean with no errors |

## Expected Final State

Response is clean with no errors

## Pass/Fail Criteria

Response contains nodes map with each requested node ID as a key
Each node object contains document field with type and name
No error messages returned
Tool completes without exception
