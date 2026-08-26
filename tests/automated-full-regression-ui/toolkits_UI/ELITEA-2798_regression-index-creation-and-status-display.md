---
id: ELITEA-2798
title: "Regression - Index Creation and Status Display"
priority: critical
type: regression
module: toolkits-indexes
status: draft
execution_type: manual
tags: [regression, smoke, toolkit-redesign, indexes]
requirements: []
---
# ELITEA-2798: Regression - Index Creation and Status Display

**Module:** Toolkits & Indexes · **Priority:** Critical · **Type:** Regression / Smoke

**Objective:** Verify index creation flow and status indicators display correctly in the redesigned UI.

**Coverage:**
- Empty state in Indexes panel
- "+ Index" button functionality
- Index creation flow
- Status indicators (in-progress, ready, error)
- Index card metadata display

## Preconditions

- Logged in to {{base_url}} with edit permissions
- A toolkit with indexing capability
- PgVector and Embedding Model configured at project level

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Any indexing-capable toolkit |
| Index Name | "regression-test-index" |
| Branch | "main" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to a toolkit with no indexes (or create new toolkit). | Indexes panel shows empty state: "No indexes created yet." |
| 2 | Click "+ Index" button. | Create Index form opens. |
| 3 | Enter Index Name: "regression-test-index", Branch: "main". | Fields accept input. |
| 4 | Click "Index" button. | Index creation starts. |
| 5 | Observe the Indexes panel. | New index card appears with spinner/in-progress indicator. |
| 6 | Wait for indexing to complete. | Status changes to green "Index is ready!" indicator. |
| 7 | Verify index card metadata. | Shows: name, created date, documents indexed count. |
| 8 | Click the index card. | Index Details page opens with correct information. |
| 9 | Verify "Index is ready!" status on details page. | Green status indicator and message visible. |

## Expected Final State

Index is created successfully with correct status indicators throughout the process.

## Pass/Fail Criteria

**Pass:**
- Empty state displays correctly
- Index creation initiates properly
- In-progress indicator shows during indexing
- Ready indicator shows when complete
- Card metadata is accurate

**Fail:**
- Missing empty state
- Create flow fails
- No/wrong status indicators
- Incorrect metadata
