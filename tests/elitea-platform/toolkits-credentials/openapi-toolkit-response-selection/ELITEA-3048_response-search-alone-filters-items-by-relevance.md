---
id: ELITEA-3048
title: "response_search Alone Filters and Ranks Items by BM25 Relevance"
priority: critical
type: functional
module: openapi-toolkit-response-selection
status: draft
execution_type: manual
tags: [feat:toolkits, int:openapi, issue:6105, api, new]
requirements: [EliteaAI/elitea_issues#6105]
---

# ELITEA-3048: response_search Alone Filters and Ranks Items by BM25 Relevance

**Module:** Toolkits & Credentials / OpenAPI Toolkit Response Selection · **Priority:** Critical · **Type:** Functional

**Objective:** Confirm supplying only `response_search` (no `response_limit`) returns items matching the query, ranked by BM25 relevance, with `ranking: "bm25"` and `result_order: "relevance"` in the `_elitea_response_selection` metadata, and the result capped at the default limit of 50 even though no explicit limit was given. Confirmed live during manual exploration ("Include search" — item-level match).

---

## Preconditions

- An OpenAPI toolkit configured against an operation returning a JSON array with a searchable text field, containing more than 50 items and at least a few items matching a chosen term.

---

## Test Data

| Field | Value |
|-------|-------|
| `response_search` | a term present in a known subset of items (e.g. `"bug"`) |
| `response_limit` | not supplied |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call the tool with only `response_search` set. | Call succeeds. |
| 2 | Inspect `_elitea_response_selection`. | `ranking: "bm25"`, `result_order: "relevance"`, `matched_items` reflects the true match count, `returned_items` ≤ 50. |
| 3 | Inspect the returned collection. | Only items relevant to the query are present, most relevant first. |

---

## Expected Final State

Item-level filtering by search term works, with BM25-ranked ordering and a default cap of 50 applied automatically.

---

## Pass/Fail Criteria

**Pass:** Matching items are returned ranked by relevance, capped at 50 by default, with correct metadata.
**Fail:** Non-matching items are included, ranking is not applied, or more than 50 items are returned without an explicit limit.
