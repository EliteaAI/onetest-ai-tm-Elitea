---
id: ELITEA-3053
title: "Quoted Phrase Requires Strict, In-Order Word Adjacency for the Phrase Boost"
priority: medium
type: functional
module: openapi-toolkit-response-selection
status: draft
execution_type: manual
tags: [feat:toolkits, int:openapi, issue:6105, api, new]
requirements: [EliteaAI/elitea_issues#6105]
---

# ELITEA-3053: Quoted Phrase Requires Strict, In-Order Word Adjacency for the Phrase Boost

**Module:** Toolkits & Credentials / OpenAPI Toolkit Response Selection · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm a quoted phrase query (e.g. `"out of memory"`) only matches/boosts items where those words appear adjacently and in that exact order — an item containing the same words scattered in unrelated positions should not receive the phrase boost, distinguishing it from a bare multi-term query. Confirmed live during the follow-up checklist pass ("quoted phrase strict adjacency").

---

## Preconditions

- An OpenAPI toolkit configured against an operation with response text containing: (a) at least one item with the exact target phrase adjacent and in order, and (b) at least one item containing the same words but not adjacent/in a different order.

---

## Test Data

| Field | Value |
|-------|-------|
| `response_search` | `"out of memory"` (quoted phrase) |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call the tool with the quoted phrase query. | Call succeeds. |
| 2 | Inspect ranking/inclusion of the item with the exact adjacent phrase. | This item receives the phrase-boost and ranks highest / is clearly prioritized. |
| 3 | Inspect ranking/inclusion of the item with the same words scattered/out of order. | This item does not receive the phrase boost — it ranks lower than the exact-phrase match, or is excluded depending on whether bare-term fallback still applies. |

---

## Expected Final State

Phrase queries are matched with true adjacency semantics, not treated as an unordered bag of words.

---

## Pass/Fail Criteria

**Pass:** Only the item with the exact adjacent, in-order phrase receives the phrase boost/top ranking.
**Fail:** An item with the same words in a different order or non-adjacent receives the same boost as the exact phrase match.
