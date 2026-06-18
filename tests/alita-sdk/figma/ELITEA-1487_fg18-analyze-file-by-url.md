---
id: ELITEA-1487
title: "FG18 - Analyze File by URL"
priority: high
type: functional
module: figma
status: ready
execution_type: automated
tags: [analyze_file, url-input, analysis, figma]
requirements: []
---
# ELITEA-1487: FG18 - Analyze File by URL

**Module:** Figma · **Priority:** High · **Type:** Functional

**Objective:** Test analyze_file using a Figma URL instead of a file key, verifying the tool can parse the URL to extract the file key and proceed with analysis.

## Preconditions

Figma toolkit is configured and authenticated
FIGMA_TOOLKIT_ID env var is set
FIGMA_FILE_URL contains a valid Figma file URL (e.g., https://www.figma.com/file/{key}/...)

## Test Data

FIGMA_TOOLKIT_ID: configured Figma toolkit ID
FIGMA_FILE_URL: https://www.figma.com/file/{valid_file_key}/File-Title
Expected file key extracted from URL: valid_file_key segment

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Figma toolkit with valid API token | Toolkit authenticated |
| 2 | Set FIGMA_FILE_URL to a valid Figma file URL in format https://www.figma.com/file/{key}/Title | URL environment variable set |
| 3 | Invoke analyze_file tool with figma_url parameter instead of file_key | Tool parses URL to extract file key |
| 4 | Validate analysis is returned successfully | Analysis result returned without error |
| 5 | Confirm result is equivalent to analysis run with the direct file key extracted from the URL | URL-based and key-based results are identical |

## Expected Final State

URL-based and key-based results are identical

## Pass/Fail Criteria

File key extracted from URL correctly
Analysis completed successfully using URL input
Result equivalent to analysis using direct file key
Tool completes without error
