---
id: ELITEA-2791
title: "Search Tool Switching Clears Previous Parameters"
priority: medium
type: functional
module: toolkits-indexes
status: ready
execution_type: manual
tags: [feat:toolkit-redesign, search, parameters]
requirements: []
---
# ELITEA-2791: Search Tool Switching Clears Previous Parameters

**Module:** Toolkits & Indexes · **Priority:** Medium · **Type:** Functional

**Objective:** Verify switching between search tools clears previous parameter values.

**Coverage:**
- Switching tools resets parameter form
- Previous tool's values are not retained
- New tool's default values are applied

## Preconditions

- Logged in to {{base_url}}
- An index with multiple search tools available

## Test Data

| Field | Value |
|-------|-------|
| Index | Any completed index |
| First Tool | Search Index |
| Second Tool | Stepback Search Index |
| Test Query | "test value" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to an index's Search page. | Search page displays. |
| 2 | Select "Search Index" tool. | Parameters for Search Index displayed. |
| 3 | Enter "test value" in the Query field. | Value is entered. |
| 4 | Adjust Cut Off slider to 0.5. | Slider value changes to 0.5. |
| 5 | Switch to "Stepback Search Index" from the Tool dropdown. | New tool parameters displayed. |
| 6 | Observe the parameter fields. | Previous values are cleared; new tool's default values shown. |
| 7 | Switch back to "Search Index". | Search Index parameters displayed. |
| 8 | Verify the Query field. | Query field is empty (not retained from previous selection). |
| 9 | Verify the Cut Off value. | Shows default value (not 0.5 from previous selection). |

## Expected Final State

Tool switching resets all parameter values to defaults for the newly selected tool.

## Pass/Fail Criteria

**Pass:**
- Switching tools clears previous values
- New tool shows its default values
- No data retention between tool switches

**Fail:**
- Previous tool's values retained after switch
- Mixed parameters from different tools
- Default values not applied
