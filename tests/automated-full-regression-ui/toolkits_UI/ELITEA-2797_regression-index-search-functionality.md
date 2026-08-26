---
id: ELITEA-2797
title: "Regression - Index Search Functionality End-to-End"
priority: critical
type: regression
module: toolkits-indexes
status: draft
execution_type: manual
tags: [regression, smoke, toolkit-redesign, search]
requirements: []
---
# ELITEA-2797: Regression - Index Search Functionality End-to-End

**Module:** Toolkits & Indexes · **Priority:** Critical · **Type:** Regression / Smoke

**Objective:** Verify the complete search workflow from Index Details through tool selection, parameter configuration, and results display.

**Coverage:**
- Search button navigation from Index Details
- Tool selection dropdown functionality
- Parameter form display and validation
- Search execution and results display
- Results panel scrolling and copy

## Preconditions

- Logged in to {{base_url}}
- A toolkit with a completed index containing searchable content

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Any toolkit with indexed content |
| Index | Completed index with documents |
| Query | "test" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Toolkit → click index card → Index Details page. | Index Details opens with Search button visible. |
| 2 | Click "Search" button. | Search page opens with two-panel layout. |
| 3 | Verify empty state shows "Select Tool" button. | Button visible with instructional text. |
| 4 | Click "Select Tool" dropdown. | Dropdown shows available tools (Search Index, etc.). |
| 5 | Select "Search Index". | Parameter form displays with Query, Filter, Cut Off, Search Top, etc. |
| 6 | Verify Query field shows required indicator (*). | Asterisk visible. |
| 7 | Click Search without entering Query. | Validation error prevents submission. |
| 8 | Enter "test" in Query field. | Value accepted. |
| 9 | Click "Search" button. | Loading indicator shows; then results appear. |
| 10 | Verify Results panel shows formatted output. | Search matches displayed with document info. |
| 11 | If results are long, verify scroll works. | Scrollbar present; all results accessible. |

## Expected Final State

Search completes successfully with results displayed in the Results panel.

## Pass/Fail Criteria

**Pass:**
- Search button navigates correctly
- Tool dropdown works
- Validation prevents empty required fields
- Search executes and returns results
- Results are scrollable

**Fail:**
- Navigation broken
- Tool selection fails
- No validation
- Search fails or no results when expected
- Results truncated
