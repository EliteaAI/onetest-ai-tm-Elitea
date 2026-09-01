---
id: ELITEA-3049
title: "response_limit Alone Previews the First N Items in Source Order, No Ranking Applied"
priority: high
type: functional
module: openapi-toolkit-response-selection
status: draft
execution_type: manual
tags: [feat:toolkits, int:openapi, issue:6105, api, new]
requirements: [EliteaAI/elitea_issues#6105]
---

# ELITEA-3049: response_limit Alone Previews the First N Items in Source Order

**Module:** Toolkits & Credentials / OpenAPI Toolkit Response Selection · **Priority:** High · **Type:** Functional

**Objective:** Confirm supplying only `response_limit` (no `response_search`) returns the first N items in their original source order, with `ranking: "none"` and `result_order: "source"` in the metadata — a plain preview, not a relevance-ranked subset. Confirmed live during manual exploration (limit-only vs search-only ranking modes).

---

## Preconditions

- An OpenAPI toolkit configured against an operation returning a JSON array with more items than the chosen limit.

---

## Test Data

| Field | Value |
|-------|-------|
| `response_search` | not supplied |
| `response_limit` | `3` |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call the tool with only `response_limit=3`. | Call succeeds. |
| 2 | Inspect `_elitea_response_selection`. | `ranking: "none"`, `result_order: "source"`. |
| 3 | Compare the 3 returned items against the unfiltered response. | They are exactly the first 3 items in original order — no reordering by relevance. |

---

## Expected Final State

`response_limit` alone behaves as a plain positional preview, distinct from the ranked behavior triggered by `response_search`.

---

## Pass/Fail Criteria

**Pass:** Returned items are the first N in original source order with `ranking: "none"`.
**Fail:** Items are reordered, ranked, or a different count than requested is returned.
