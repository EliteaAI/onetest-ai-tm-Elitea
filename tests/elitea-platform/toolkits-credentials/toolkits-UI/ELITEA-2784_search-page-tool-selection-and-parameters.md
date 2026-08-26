---
id: ELITEA-2784
title: "Search Page - Tool Selection and Parameter Display"
priority: critical
type: functional
module: toolkits-indexes
status: ready
execution_type: manual
tags: [feat:toolkit-redesign, smoke, search, parameters]
requirements: []
---
# ELITEA-2784: Search Page - Tool Selection and Parameter Display

**Module:** Toolkits & Indexes · **Priority:** Critical · **Type:** Functional / Smoke

**Objective:** Verify tool selection dropdown and parameter display on the Search page.

**Coverage:**
- Tool selector dropdown shows available tools
- Selecting a tool displays tool-specific parameters
- Required parameters show asterisk (*) indicator
- Info icons show tooltips on hover

## Preconditions

- Logged in to {{base_url}}
- A toolkit with a completed index that has search tools available

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Any toolkit with index search capability |
| Index | Completed index |
| Tool | Search Index |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to an index's Search page. | Search page displays with empty state. |
| 2 | Click the "Select Tool" button/dropdown. | Dropdown opens showing available tools (e.g., "Search Index", "Stepback Search Index", "Stepback Summary Index"). |
| 3 | Observe the dropdown has a search/filter field. | Search field visible at top of dropdown. |
| 4 | Select "Search Index" from the dropdown. | Tool is selected; parameter form appears in Search Settings panel. |
| 5 | Observe the "Tool" field. | Shows "Search Index" with dropdown indicator. |
| 6 | Verify "Query" field shows asterisk (*) indicating required. | "Query *" label visible with required indicator. |
| 7 | Hover over the info icon (i) next to "Query". | Tooltip displays description of the Query parameter. |
| 8 | Observe other parameters displayed. | Parameters visible: Filter, Cut Off (0-1) slider with value, Search Top, Full Text Search, Extended Search. |
| 9 | Verify the "Cut Off" slider shows current value (e.g., 0.1). | Slider with numeric value displayed. |
| 10 | Verify "Search Top" shows default value (e.g., 10). | Default value displayed. |

## Expected Final State

Search Settings panel displays the selected tool with all parameters, required field indicators, and info tooltips working correctly.

## Pass/Fail Criteria

**Pass:**
- Tool dropdown shows all available search tools
- Selecting tool displays correct parameters
- Required fields show asterisk indicator
- Info tooltips display on hover
- Slider and input fields function correctly

**Fail:**
- Tool dropdown empty or missing tools
- Parameters don't display after tool selection
- No required field indicators
- Tooltips missing or incorrect
