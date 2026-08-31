---
id: ELITEA-2987
title: "ADO Work Item Text Search – search_work_items_by_text -> get_work_item Chain Works End-to-End"
priority: high
type: functional
module: ado
status: draft
execution_type: manual
tags: [sdk, ado, toolkit, work-items, text-search, issue:6104]
requirements: [EliteaAI/elitea_issues#6104]
---

# ELITEA-2987: ADO Work Item Text Search – search_work_items_by_text -> get_work_item Chain Works End-to-End

**Module:** Ado · **Priority:** High · **Type:** Functional

**Objective:** Verify a result's `id` from `search_work_items_by_text` can be fed directly into `get_work_item` to retrieve the full work item.

---

## Preconditions

- ADO Board toolkit is configured with valid credentials, exposing both `search_work_items_by_text` and `get_work_item`.

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call `search_work_items_by_text` with a query matching at least one work item | Call succeeds, at least one result returned |
| 2 | Take the `id` of the first result and call `get_work_item` with it | Call succeeds |
| 3 | Compare the full work item's title/type/state to the search result's summary fields | Values match (same underlying work item) |

---

## Expected Final State

The two tools compose correctly — a search result's `id` is a valid, immediately usable input to `get_work_item`.

---

## Pass/Fail Criteria

**Pass:** `get_work_item` succeeds using the search result's `id`, and returned details are consistent with the search summary.
**Fail:** `get_work_item` fails with that `id`, or returned details are inconsistent with the search result.
