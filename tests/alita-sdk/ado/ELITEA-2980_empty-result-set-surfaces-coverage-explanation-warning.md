---
id: ELITEA-2980
title: "ADO Work Item Text Search – A Genuinely Empty Result Set Produces a Search-Coverage-Explanation Warning"
priority: medium
type: functional
module: ado
status: draft
execution_type: manual
tags: [sdk, ado, toolkit, work-items, text-search, issue:6104]
requirements: [EliteaAI/elitea_issues#6104]
---

# ELITEA-2980: ADO Work Item Text Search – A Genuinely Empty Result Set Produces a Search-Coverage-Explanation Warning

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when a query simply matches nothing (no info code involved — a plain zero-hit search), the response still includes a warning explaining possible reasons for the empty result (e.g. search index coverage/latency), distinct from the filter-specific warning in ELITEA-2979.

---

## Preconditions

- ADO Board toolkit is configured with valid credentials.

---

## Test Data

| Field | Value |
|-------|-------|
| query | A random, highly unlikely-to-match string, e.g. a UUID |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call `search_work_items_by_text` with the random query, no filters | Call succeeds, `total_count=0` |
| 2 | Inspect the response for a warning field | A generic search-coverage-explanation warning is present (not the filter-specific ELITEA-2979 message) |

---

## Expected Final State

A plain zero-hit query returns a helpful, generically-worded warning about possible causes.

---

## Pass/Fail Criteria

**Pass:** A coverage-explanation warning is present on genuinely empty results.
**Fail:** No warning is surfaced for an empty result set, or the wrong (filter-specific) warning is shown instead.
