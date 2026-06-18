---
id: ELITEA-1485
title: "FG12 - Get File Images (Custom Format and Scale)"
priority: medium
type: functional
module: figma
status: ready
execution_type: automated
tags: [get_file_images, images, format, scale, figma]
requirements: []
---
# ELITEA-1485: FG12 - Get File Images (Custom Format and Scale)

**Module:** Figma · **Priority:** Medium · **Type:** Functional

**Objective:** Test get_file_images with different export formats (PNG, SVG) and custom scaling factor, verifying format and scale parameters are applied correctly.

## Preconditions

Figma toolkit is configured and authenticated
FIGMA_TOOLKIT_ID, FIGMA_FILE_KEY, and FIGMA_NODE_IDS env vars are set
Target nodes are renderable

## Test Data

FIGMA_TOOLKIT_ID: configured Figma toolkit ID
FIGMA_FILE_KEY: valid Figma file key
FIGMA_NODE_IDS: comma-separated list of renderable node IDs
format: "svg"
scale: 2

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Figma toolkit with valid API token | Toolkit authenticated |
| 2 | Set FIGMA_FILE_KEY and FIGMA_NODE_IDS to valid values | Environment variables set |
| 3 | Invoke get_file_images with file_key, ids, format="svg", and scale=2 | API request sent with SVG format and 2x scale parameters |
| 4 | Validate response contains image URLs for requested nodes | Images map returned successfully |
| 5 | Verify URLs correspond to SVG format images | SVG format applied as specified |
| 6 | Confirm scaled images are returned correctly | 2x scale successfully applied |

## Expected Final State

2x scale successfully applied

## Pass/Fail Criteria

Images returned in specified format (SVG or PNG)
Custom scale applied to images
URLs differ from default (1x PNG) call
Tool completes without error
