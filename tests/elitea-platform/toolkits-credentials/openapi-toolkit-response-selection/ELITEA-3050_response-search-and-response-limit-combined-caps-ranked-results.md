---
id: ELITEA-3050
title: "response_search and response_limit Combined Cap Applies After Ranking"
priority: critical
type: functional
module: openapi-toolkit-response-selection
status: draft
execution_type: manual
tags: [feat:toolkits, int:openapi, issue:6105, api, new]
requirements: [EliteaAI/elitea_issues#6105]
---

# ELITEA-3050: response_search and response_limit Combined Cap Applies After Ranking

**Module:** Toolkits & Credentials / OpenAPI Toolkit Response Selection · **Priority:** Critical · **Type:** Functional

**Objective:** Confirm using `response_search` and `response_limit` together returns only the top-N BM25-ranked items (limit applied post-filter/ranking, not pre-filter), with items returned unmodified inside the original array/map envelope. Confirmed live during manual exploration ("Search + limit" — cap enforced post-filter).

---

## Preconditions

- An OpenAPI toolkit configured against an operation whose response contains 3+ items matching a chosen query term.

---

## Test Data

| Field | Value |
|-------|-------|
| `response_search` | a term matching 3+ items |
| `response_limit` | `2` |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call the tool with both arguments set. | Call succeeds. |
| 2 | Inspect the returned collection. | Exactly 2 items are returned — the top-2 ranked by relevance, not simply the first 2 matches in source order. |
| 3 | Compare each returned item field-for-field against the corresponding item in the unfiltered response. | Items are byte-identical to their source form — no projection into a new synthetic shape. |
| 4 | Inspect metadata. | `matched_items` reflects the full match count (e.g. 3+), `returned_items` is 2, `truncated: true`. |

---

## Expected Final State

The limit caps the ranked result set, not the raw match set; original item objects are preserved unmodified.

---

## Pass/Fail Criteria

**Pass:** Top-2 ranked matches returned, unmodified, with correct `matched_items`/`returned_items`/`truncated` metadata.
**Fail:** Wrong items are returned (e.g. first-2 in source order instead of top-2 ranked), or items are altered from their original shape.
