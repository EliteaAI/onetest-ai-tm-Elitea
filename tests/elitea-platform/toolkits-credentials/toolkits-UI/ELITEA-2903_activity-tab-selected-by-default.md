---
id: ELITEA-2903
title: "Index Details — Activity Tab Selected by Default"
priority: critical
type: functional
module: toolkits-indexes
status: draft
execution_type: manual
tags: [feat:toolkit-redesign, indexes, tabs, default-state]
requirements: []
---
# ELITEA-2903: Index Details — Activity Tab Selected by Default

**Module:** Toolkits & Indexes · **Priority:** Critical · **Type:** Functional

**Objective:** Verify "Activity" is selected by default immediately after Index creation and on every fresh navigation to the Index details page, and that a manual tab switch persists only while the user remains on the page during that visit.

**Coverage:**
- "Activity" default immediately after creation
- "Activity" default on fresh navigation to an existing Index
- Manual tab selection persists through an unrelated in-page action during the same visit
- Manual tab selection does not persist after leaving and reopening the Index (fresh navigation resets to "Activity")

## Preconditions

- Logged in to {{base_url}} with edit permissions
- A toolkit that supports indexing and has valid source data available

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Any indexable toolkit with valid source data |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a new Index on the toolkit. | Index is created and its details page opens. |
| 2 | Inspect which tab is selected. | "Activity" is selected. |
| 3 | Click "Configuration". | "Configuration" becomes selected. |
| 4 | Scroll the page and hover over an unrelated element, without switching tabs. | "Configuration" remains selected. |
| 5 | Navigate to the Toolkits & Indexes list. | List page displays. |
| 6 | Open the same Toolkit, then open the same Index. | Index details page opens. |
| 7 | Inspect which tab is selected. | "Activity" is selected again, not "Configuration". |

## Expected Final State

"Activity" is the default tab on creation and on every fresh navigation; a manually selected tab persists only for the duration of the current visit.

## Pass/Fail Criteria

**Pass:**
- "Activity" is selected after creation and after each fresh navigation
- A manually selected tab remains selected through unrelated in-page actions during the same visit
- A manually selected tab does not remain selected after navigating away and back

**Fail:**
- Any tab other than "Activity" is selected after creation or after a fresh navigation
- A manually selected tab reverts during the same visit without navigating away
- A manually selected tab remains selected after navigating away and back
