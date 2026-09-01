---
id: ELITEA-3051
title: "Exclusion Term (-word) Removes Matching Items From the Result Set"
priority: high
type: functional
module: openapi-toolkit-response-selection
status: draft
execution_type: manual
tags: [feat:toolkits, int:openapi, issue:6105, api, new]
requirements: [EliteaAI/elitea_issues#6105]
---

# ELITEA-3051: Exclusion Term (-word) Removes Matching Items From the Result Set

**Module:** Toolkits & Credentials / OpenAPI Toolkit Response Selection · **Priority:** High · **Type:** Functional

**Objective:** Confirm a hard-exclusion term (e.g. `active -archived`) removes any item whose searchable text contains the excluded word, regardless of how well it otherwise matches the positive terms. Also confirm an exclusion-only query (no positive term, e.g. `-archived`) is honored — items are filtered out without a positive term required. Confirmed live during manual exploration ("Exclude search" — complementary to include; follow-up "exclusion-only query").

---

## Preconditions

- An OpenAPI toolkit configured against an operation returning items where some contain a distinguishing excludable word (e.g. "archived") and some do not.

---

## Test Data

| Field | Value |
|-------|-------|
| Query A (combined) | `active -archived` |
| Query B (exclusion-only) | `-archived` |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call with `response_search="active -archived"`. | No returned item's searchable text contains "archived", even if it otherwise matches "active" strongly. |
| 2 | Call with `response_search="-archived"` (exclusion term only, no positive term). | Items containing "archived" are excluded; all other items are considered (not zero-matched merely for lacking a positive term). |

---

## Expected Final State

Exclusion terms reliably filter out matching items whether combined with positive terms or used alone.

---

## Pass/Fail Criteria

**Pass:** Both combined and exclusion-only queries correctly omit items containing the excluded term.
**Fail:** An excluded-term item still appears in results, or an exclusion-only query is rejected/mishandled instead of filtering normally.
