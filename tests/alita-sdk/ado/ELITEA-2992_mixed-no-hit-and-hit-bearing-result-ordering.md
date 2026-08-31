---
id: ELITEA-2992
title: "ADO Work Item Text Search – Mixed No-Hit/Hit-Bearing Result Ordering for Highlight Assignment"
priority: medium
type: functional
module: ado
status: draft
execution_type: manual
tags: [sdk, ado, toolkit, work-items, text-search, issue:6104, new]
requirements: [EliteaAI/elitea_issues#6104]
---

# ELITEA-2992: ADO Work Item Text Search – Mixed No-Hit/Hit-Bearing Result Ordering for Highlight Assignment

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Deliberately construct a result set where the first 1–2 ranked results have no field-level highlight matches and later results do, to properly exercise and validate the highlight-budget evaluation-order logic covered speculatively in [[ELITEA-2985]] — prior exploratory test data was homogeneous by chance and never exercised this path.

---

## Preconditions

- ADO Board toolkit is configured with valid credentials.
- Test data or a query is deliberately engineered so relevance ranking places at least one non-hit-bearing result ahead of hit-bearing ones (e.g. a title-only relevance match ranked above richer content matches, or by choosing a query term that appears in a field ADO ranks highly but that isn't a highlightable field).

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Run the query with `include_highlights=false` first and inspect result order/fields to confirm the mixed ordering exists | At least one of the first 2 results has no highlightable field match |
| 2 | Re-run with `include_highlights=true` | Call succeeds |
| 3 | Verify highlights are assigned only to results that actually have hits, and the withheld-count warning (if shown) reflects the true count of hit-bearing results beyond the 5th | Correct, no false "withheld" warning triggered by non-hit-bearing leading results |

---

## Expected Final State

Highlight assignment logic correctly skips non-hit-bearing results without consuming budget or miscounting withheld results.

---

## Pass/Fail Criteria

**Pass:** Highlight budget and withheld-count warning are accurate in this deliberately mixed scenario.
**Fail:** A non-hit-bearing leading result consumes budget, or the withheld-count warning is inaccurate.
