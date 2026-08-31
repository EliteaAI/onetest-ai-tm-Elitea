---
id: ELITEA-2985
title: "ADO Work Item Text Search – Highlight Budget Is Spent in Evaluation Order, Not Only on Hit-Bearing Results"
priority: medium
type: functional
module: ado
status: draft
execution_type: manual
tags: [sdk, ado, toolkit, work-items, text-search, issue:6104, inconclusive]
requirements: [EliteaAI/elitea_issues#6104]
---

# ELITEA-2985: ADO Work Item Text Search – Highlight Budget Is Spent in Evaluation Order, Not Only on Hit-Bearing Results

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the "first 5 hit-bearing results" highlight budget is spent by walking results in their normal evaluation (ranking) order, so a leading result with no field-level hits doesn't cause a false "withheld" warning or get skipped incorrectly. **Status: previously untested — exploratory testing only produced homogeneous data where every result happened to have hits.**

---

## Preconditions

- ADO Board toolkit is configured with valid credentials.
- A query is constructed (or test data arranged) so that the first 1–2 ranked results have no field-level text match while later results do (e.g. via ADO's relevance ranking putting a title-only match ahead of a richer content match, or vice versa).

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Construct/identify a query where the top-ranked result(s) have no highlight-worthy field hits | Test data confirmed via a baseline call with `include_highlights=false` |
| 2 | Call with `include_highlights=true` | Call succeeds |
| 3 | Inspect which results carry `highlights` and the withheld-count warning | Highlights are correctly assigned to the actual hit-bearing results in ranking order; the withheld count matches the true number of hit-bearing results beyond the 5th, not an inflated/wrong count caused by counting non-hit-bearing leading results |

---

## Expected Final State

The 5-result highlight budget is spent strictly against hit-bearing results in evaluation order; non-hit-bearing results never consume budget or cause an inaccurate withheld count.

---

## Pass/Fail Criteria

**Pass:** Highlight assignment and the withheld-count warning are both correct even when leading results have no hits.
**Fail:** A leading non-hit-bearing result consumes highlight budget, or the withheld-count warning is inaccurate in this scenario.
