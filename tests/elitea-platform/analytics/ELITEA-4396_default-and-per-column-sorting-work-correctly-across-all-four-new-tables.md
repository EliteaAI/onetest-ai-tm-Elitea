---
id: ELITEA-4396
title: "Default sort and per-column sorting work correctly on Versions, Models, Trigger Sources, and Recent Runs"
priority: high
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, issue:7033, r-2.0.8, agent-pipeline-analytics, sorting]
requirements: [EliteaAI/elitea_issues#7033]
---

# ELITEA-4396: Default sort and per-column sorting work correctly on Versions, Models, Trigger Sources, and Recent Runs

**Module:** Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify each of the four new tables applies its specified default sort on load, that clicking any column header toggles ascending/descending and sorts by underlying numeric/date values (not formatted strings), and that for Recent Runs with multiple pages, sorting is applied server-side across the full dataset rather than only the currently-loaded page.

**Coverage:**
- Default sorts: Versions RUNS desc, Models TOTAL TOKENS desc, Trigger Sources RUNS desc, Recent Runs STARTED desc
- Per-column sort toggle (asc/desc) using underlying values, not string ordering (e.g. "10" sorts after "2", not before)
- Server-side sort applied before pagination for Recent Runs across the full dataset

## Preconditions

- Logged in to `{{base_url}}`
- An Agent or Pipeline with enough Versions, Models, and Trigger Sources rows to meaningfully verify sort order, and enough runs in Recent Runs to span multiple pages

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Entity | Agent or Pipeline with multi-page Recent Runs and multiple rows in each of the other three tables |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the detail view and check the default sort order of Versions, Models, Trigger Sources, and Recent Runs on initial load (no user interaction) | Versions sorted by RUNS desc; Models sorted by TOTAL TOKENS desc; Trigger Sources sorted by RUNS desc; Recent Runs sorted by STARTED desc |
| 2 | Click the RUNS column header in Versions once, then again | Toggles between ascending and descending order; order is numerically correct (e.g., a row with RUNS=10 sorts after RUNS=2 in ascending order, not alphabetically before it) |
| 3 | Repeat column-header sort toggling for at least one other column in each of Models, Trigger Sources, and Recent Runs (e.g. TOTAL TOKENS, COST, STARTED) | Each toggles asc/desc correctly using underlying numeric/date values |
| 4 | In Recent Runs (with multiple pages), sort by a column (e.g. COST) then page forward through all pages | Sort order is correct and consistent across the full paginated dataset, not reset or limited to only the first page's rows |

## Expected Final State

All four tables default to their specified sort order on load, every sortable column toggles ascending/descending correctly using underlying values, and sorting in Recent Runs applies across the full dataset regardless of pagination.

## Pass/Fail Criteria

**Pass:**
- All four default sorts match spec exactly
- Column header clicks toggle sort direction and order numeric/date values correctly (not as strings)
- Recent Runs sort is applied across the entire filtered dataset, consistent across all pages

**Fail:**
- Any default sort is wrong or missing
- Any column sorts as string rather than numeric/date value (e.g. "10" before "2")
- Recent Runs sort only applies to the currently-loaded page, producing inconsistent order across pages
