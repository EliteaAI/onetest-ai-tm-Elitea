---
id: ELITEA-2960
title: "Regression: Stepback Search and Stepback Summary Tools Execute and Render Correctly"
priority: high
type: regression
module: toolkits-indexes
status: draft
execution_type: manual
tags: [regression, toolkit-redesign, search]
requirements: []
---
# ELITEA-2960: Regression: Stepback Search and Stepback Summary Tools Execute and Render Correctly

**Module:** Toolkits & Indexes · **Priority:** High · **Type:** Regression

**Objective:** Verify that, in addition to "Search Index" (already covered by ELITEA-2784/2785/2791), the "Stepback Search Index" and "Stepback Summary Index" tools each display their own correct Search Settings parameters when selected, execute successfully, and render the appropriate result type in Results — re-validating legacy per-tool search behavior (ELITEA-1243 and related) inside the redesigned Search page.

**Coverage:**
- Selecting "Stepback Search Index" displays its own parameters; a broader/contextual query returns a contextually related result in Results
- Selecting "Stepback Summary Index" displays its own parameters; a topic query returns a summary-style response in Results
- Switching from one Stepback tool to the other replaces the displayed parameters with the newly selected tool's own set — no leftover fields/values from the previous tool

## Preconditions

- Logged in to {{base_url}} with edit permissions
- An existing Index with completed indexing data compatible with both Stepback search tools

## Test Data

| Field | Value |
|-------|-------|
| Index | A completed Index |
| Contextual query | A broader/contextual query relevant to the indexed content (for Stepback Search Index) |
| Topic query | A topic query relevant to the indexed content (for Stepback Summary Index) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Index's Search page and click "Select Tool". | Tool list opens. |
| 2 | Select "Stepback Search Index". | Search Settings displays the parameters specific to Stepback Search Index. |
| 3 | Enter the broader/contextual query. | Value is accepted. |
| 4 | Click "Search". | Results panel shows a loading state, then renders a contextually related result via the standard Elitea response component. |
| 5 | Click "Select Tool" and select "Stepback Summary Index". | Search Settings now displays the parameters specific to Stepback Summary Index — none of Stepback Search Index's prior field values remain. |
| 6 | Enter the topic query. | Value is accepted. |
| 7 | Click "Search". | Results panel shows a loading state, then renders a summary-style response. |

## Expected Final State

Both Stepback search tools independently display their own correct parameters when selected, execute successfully, and render the appropriate result type in Results.

## Pass/Fail Criteria

**Pass:**
- Each Stepback tool's own parameters display correctly when selected, with no residual fields/values from the other tool
- "Stepback Search Index" returns a contextually related result for a broader query
- "Stepback Summary Index" returns a summary-style response for a topic query

**Fail:**
- A tool's parameters fail to display, display incorrectly, or retain values from the other Stepback tool
- Either tool fails to execute, returns an incorrect result type, or fails to render via the standard response component
