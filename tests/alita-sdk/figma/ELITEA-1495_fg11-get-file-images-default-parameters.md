---
id: ELITEA-1495
title: "FG11 - Get File Images (Default Parameters)"
priority: high
type: functional
module: figma
status: ready
execution_type: automated
tags: [get_file_images, images, smoke, figma]
requirements: []
---
# ELITEA-1495: FG11 - Get File Images (Default Parameters)

**Module:** Figma · **Priority:** High · **Type:** Functional

**Objective:** Test get_file_images with default parameters, retrieving rendered image URLs for specified node IDs using the default format and scale.

## Preconditions

Figma toolkit is configured and authenticated
FIGMA_TOOLKIT_ID, FIGMA_FILE_KEY, and FIGMA_NODE_IDS env vars are set
Target nodes are renderable in the file

## Test Data

FIGMA_TOOLKIT_ID: configured Figma toolkit ID
FIGMA_FILE_KEY: valid Figma file key
FIGMA_NODE_IDS: comma-separated list of renderable node IDs

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Figma toolkit with valid API token | Toolkit authenticated |
| 2 | Set FIGMA_FILE_KEY and FIGMA_NODE_IDS to valid values | Environment variables set |
| 3 | Invoke get_file_images tool with file_key and ids parameters (no format or scale) | API request sent with default format and scale |
| 4 | Validate response contains images map with requested node IDs as keys | Images map returned for all requested nodes |
| 5 | Verify each map value is a string URL pointing to a Figma CDN image | Valid image URLs returned |
| 6 | Confirm default PNG format by checking URL or response metadata | PNG format applied by default |

## Expected Final State

PNG format applied by default

## Pass/Fail Criteria

Images map returned with node IDs as keys
Each value is a valid image CDN URL
Default format PNG applied
Default scale (1x) applied
Tool completes without error
