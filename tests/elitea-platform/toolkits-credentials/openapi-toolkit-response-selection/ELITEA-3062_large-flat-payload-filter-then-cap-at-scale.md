---
id: ELITEA-3062
title: "Large Flat Payload (100+ Items) Is Filtered Then Capped Correctly at Scale"
priority: medium
type: functional
module: openapi-toolkit-response-selection
status: draft
execution_type: manual
tags: [feat:toolkits, int:openapi, issue:6105, api, new, performance]
requirements: [EliteaAI/elitea_issues#6105]
---

# ELITEA-3062: Large Flat Payload (100+ Items) Is Filtered Then Capped Correctly at Scale

**Module:** Toolkits & Credentials / OpenAPI Toolkit Response Selection · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm filtering and capping behave correctly at scale against a large flat-array response (100+ items) — the full set is scored/filtered, and only then is the limit applied to the ranked subset. Confirmed live during manual exploration ("huge payload, 100 VSCode issues" — filter-then-cap at scale).

---

## Preconditions

- An OpenAPI toolkit configured against an operation known to return 100+ items in a flat array (e.g. a large public issue-tracker search API).

---

## Test Data

| Field | Value |
|-------|-------|
| `response_search` | a term matching a meaningful subset of the 100+ items |
| `response_limit` | e.g. `10` |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call the tool against the large dataset with search + limit set. | Call succeeds without timeout/error. |
| 2 | Inspect `matched_items` vs `returned_items`. | `matched_items` reflects the true match count across all 100+ items (not just the first N scanned); `returned_items` equals the limit (or fewer if matches < limit). |
| 3 | Spot-check returned items' relevance. | Top-ranked items are genuinely the most relevant among the full matched set, not merely the first N encountered. |

---

## Expected Final State

Filtering/ranking correctly considers the entire response before the limit is applied, even at 100+ item scale.

---

## Pass/Fail Criteria

**Pass:** Full-set matching and correct top-N selection confirmed at scale.
**Fail:** Matching or ranking appears to only consider a partial prefix of the data, or performance/timeout issues occur.
