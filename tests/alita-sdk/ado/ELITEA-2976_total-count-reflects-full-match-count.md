---
id: ELITEA-2976
title: "ADO Work Item Text Search – total_count Reflects the Full Match Count, Not Just the Current Window"
priority: high
type: functional
module: ado
status: draft
execution_type: manual
tags: [sdk, ado, toolkit, work-items, text-search, issue:6104]
requirements: [EliteaAI/elitea_issues#6104]
---

# ELITEA-2976: ADO Work Item Text Search – total_count Reflects the Full Match Count, Not Just the Current Window

**Module:** Ado · **Priority:** High · **Type:** Functional

**Objective:** Verify `total_count` always reflects the full number of matches across the entire result set, not merely the number of items returned in the current page.

---

## Preconditions

- ADO Board toolkit is configured with valid credentials.
- A query matches more items than the default/requested `top`.

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call with `top=5` against a query known to match more than 5 items | `returned=5`, `total_count` equals the true full match count (>5) |
| 2 | Call the same query with `top=50` | `returned` grows toward the total (bounded by 50), `total_count` stays the same as step 1 |

---

## Expected Final State

`total_count` is stable across different `top` values for the same query and reflects the true total.

---

## Pass/Fail Criteria

**Pass:** `total_count` matches the true full match count and does not vary with `top`.
**Fail:** `total_count` equals `returned` (i.e. it's just echoing the page size) or varies inconsistently with `top`.
