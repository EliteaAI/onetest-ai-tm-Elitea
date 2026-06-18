---
id: ELITEA-1480
title: "FG17 - Analyze File with Filters"
priority: medium
type: functional
module: figma
status: ready
execution_type: automated
tags: [analyze_file, page-filter, analysis, filters, figma]
requirements: []
---
# ELITEA-1480: FG17 - Analyze File with Filters

**Module:** Figma · **Priority:** Medium · **Type:** Functional

**Objective:** Test analyze_file with specific page filtering and with design insights disabled, verifying that page filter limits analysis to specified pages and insights flag controls output.

## Preconditions

Figma toolkit is configured and authenticated
FIGMA_TOOLKIT_ID and FIGMA_FILE_KEY env vars are set
File has multiple pages; target page name known

## Test Data

FIGMA_TOOLKIT_ID: configured Figma toolkit ID
FIGMA_FILE_KEY: valid multi-page Figma file key
pages filter: ["Page 1"] (or specific page name)
include_design_insights: false

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Figma toolkit with valid API token | Toolkit authenticated |
| 2 | Set FIGMA_FILE_KEY to a file with multiple pages; note at least one page name | Environment variable set and page names known |
| 3 | Invoke analyze_file with file_key, pages=["Page 1"] filter, and include_design_insights=false | Analysis request sent with page filter and no-insights flag |
| 4 | Validate response only includes analysis of the specified page | Analysis is scoped to Page 1 only |
| 5 | Verify design insights section is absent or empty in response | Design insights excluded as requested |
| 6 | Compare against full default analysis to confirm filtering effect | Filtered result is smaller/different than default |

## Expected Final State

Filtered result is smaller/different than default

## Pass/Fail Criteria

Analysis scoped to specified page only (not full file)
Design insights section absent or empty when disabled
Filtered result is smaller/different than default full analysis
Tool completes without error
