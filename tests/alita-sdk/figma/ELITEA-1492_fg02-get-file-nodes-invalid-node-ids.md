---
id: ELITEA-1492
title: "FG02 - Get File Nodes (Invalid Node IDs)"
priority: high
type: functional
module: figma
status: ready
execution_type: automated
tags: [get_file_nodes, edge-case, negative, nodes, figma]
requirements: []
---
# ELITEA-1492: FG02 - Get File Nodes (Invalid Node IDs)

**Module:** Figma · **Priority:** High · **Type:** Functional

**Objective:** Test get_file_nodes behavior with invalid node IDs, verifying graceful error handling or partial results when node IDs do not exist in the file.

## Preconditions

Figma toolkit is configured and authenticated
FIGMA_TOOLKIT_ID and FIGMA_FILE_KEY env vars are set
NEGATIVE test — node IDs used do not exist in the target file

## Test Data

FIGMA_TOOLKIT_ID: configured Figma toolkit ID
FIGMA_FILE_KEY: valid Figma file key
Invalid node IDs used: "INVALID_NODE_1,INVALID_NODE_2" (non-existent in file)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Figma toolkit with valid API token | Toolkit authenticated |
| 2 | Set FIGMA_FILE_KEY to a valid file key | Environment variable set |
| 3 | Set node IDs to non-existent values (e.g., "INVALID_NODE_1,99999:99999") | Invalid node IDs prepared |
| 4 | Invoke get_file_nodes tool with the invalid node_ids | Tool executes and sends API request with invalid IDs |
| 5 | Validate the response handles the invalid nodes gracefully (error message or null entries) | Response indicates nodes not found or returns empty node map |
| 6 | Confirm no unhandled exception is raised | Tool exits cleanly without stack trace |

## Expected Final State

Tool exits cleanly without stack trace

## Pass/Fail Criteria

Tool returns error message or empty nodes map for invalid IDs
No unhandled Python exception or stack trace
Response is gracefully handled
