---
id: ELITEA-1062
title: "Sorting in Agents/Pipelines Tables Across Pagination"
priority: high
type: functional
module: tables
status: draft
execution_type: manual
tags: [pagination, pipelines, sorting, agents, ui]
requirements: []
---
# ELITEA-1062: Sorting in Agents/Pipelines Tables Across Pagination

**Module:** Tables · **Priority:** High · **Type:** Functional

**Objective:** Verify that sorting in Agents and Pipelines tables works correctly across the entire dataset, not just the currently loaded page. When users sort by any column, the system should fetch and display sorted data from the complete dataset (all pages), not just re-sort the already loaded rows.

## Preconditions

- User logged in to Elitea stage environment
- Multiple agents/pipelines created (at least 50 to span multiple pages)
- User has permissions to view agents and pipelines
- Default pagination: 20 items per page

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agents page | Agents table loads with first 20 agents (page 1) |
| 2 | Click column header to sort by Name (A-Z) | Table displays first 20 agents sorted by Name across ENTIRE dataset, not just current page |
| 3 | Navigate to page 2 | Page 2 shows agents 21-40 in globally sorted order (names continue alphabetically from page 1) |
| 4 | Navigate back to page 1 and sort by Date Created (newest first) | Table displays newest 20 agents from entire dataset, not just re-sorting page 1 content |
| 5 | Change page size to 50 items per page | Sorting persists, shows first 50 agents in current sort order from global dataset |
| 6 | Repeat steps 1-5 for Pipelines page | Pipelines table behaves identically - sorting works across full dataset, not per-page |

## Expected Final State

Pipelines table behaves identically - sorting works across full dataset, not per-page

## Pass/Fail Criteria

PASS: Sorting triggers backend query with ORDER BY clause, pagination shows globally sorted data
FAIL: Sorting only re-orders currently loaded rows, next page shows unsorted or incorrectly sorted data
