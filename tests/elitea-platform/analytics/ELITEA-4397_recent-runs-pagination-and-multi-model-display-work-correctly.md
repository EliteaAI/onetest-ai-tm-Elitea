---
id: ELITEA-4397
title: "Recent Runs pagination behaves correctly and multi-model runs show all models in the MODEL column"
priority: high
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, issue:7033, r-2.0.8, agent-pipeline-analytics, recent-runs, pagination, multi-model]
requirements: [EliteaAI/elitea_issues#7033]
---

# ELITEA-4397: Recent Runs pagination behaves correctly and multi-model runs show all models in the MODEL column

**Module:** Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify Recent Runs pagination controls behave consistently with other Analytics tables (correct rows per page, no duplicates/gaps when paging, page-size changes update row count if configurable), and that a multi-model run's MODEL column shows all models used — either directly or via an expandable/compact summary — never arbitrarily truncated to a single model.

**Coverage:**
- Pagination forward/backward with no duplicate or missing rows
- Page-size change (if configurable) updates displayed row count accordingly
- MODEL column for a multi-model run shows every model used, with no silent omission

## Preconditions

- Logged in to `{{base_url}}`
- An Agent or Pipeline with enough runs to span at least 2 pages of Recent Runs
- At least one multi-model run present within that run history

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Entity | Agent or Pipeline with multi-page run history including a multi-model run |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the detail view and locate Recent Runs; record the run identifiers/timestamps shown on page 1 | Page 1 rows recorded |
| 2 | Page forward to page 2 | Different rows load; no row from page 1 reappears on page 2 (no duplicates) |
| 3 | Page backward to page 1 | Original page-1 rows reload exactly, with no gaps or missing rows |
| 4 | If page size is configurable, change it and observe the table | Row count per page updates accordingly, and the full dataset is still reachable via paging |
| 5 | Locate the multi-model run (search across pages if necessary) and inspect its MODEL column value | All models used in that run are shown — either listed directly or via an expandable/compact summary that provides access to the full list |
| 6 | Confirm no model used in that run is missing from the displayed value or its expanded view | Every model actually used appears somewhere in the MODEL column's display or expansion |

## Expected Final State

Recent Runs pagination produces a complete, non-duplicated traversal of all runs in the filtered dataset, and the MODEL column for multi-model runs never silently hides any model actually used.

## Pass/Fail Criteria

**Pass:**
- Paging forward/backward produces correct rows with no duplicates or gaps
- Page-size changes (if supported) correctly adjust displayed row count
- Multi-model run's MODEL column shows or provides access to every model used

**Fail:**
- Paging produces duplicate rows, skipped rows, or inconsistent counts
- Page-size change does not take effect
- A multi-model run's MODEL column omits any model that was actually used
