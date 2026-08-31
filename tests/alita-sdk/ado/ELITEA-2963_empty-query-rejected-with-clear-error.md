---
id: ELITEA-2963
title: "ADO Work Item Text Search – Empty/Blank Query Rejected With a Clear Tool Error"
priority: high
type: functional
module: ado
status: draft
execution_type: manual
tags: [sdk, ado, toolkit, work-items, text-search, issue:6104]
requirements: [EliteaAI/elitea_issues#6104]
---

# ELITEA-2963: ADO Work Item Text Search – Empty/Blank Query Rejected With a Clear Tool Error

**Module:** Ado · **Priority:** High · **Type:** Functional

**Objective:** Verify an empty or blank `query` is rejected with a clear tool error, and no call is made to Azure DevOps.

---

## Preconditions

- ADO Board toolkit is configured with valid credentials.

---

## Test Data

| Field | Value |
|-------|-------|
| query (case A) | `""` (empty string) |
| query (case B) | `"   "` (whitespace-only) |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call `search_work_items_by_text` with `query=""` | Tool returns a clear validation error, no ADO API call is made |
| 2 | Call `search_work_items_by_text` with `query="   "` | Same clear validation error, no ADO API call is made |

---

## Expected Final State

Neither call reaches Azure DevOps; both fail fast with an actionable error message.

---

## Pass/Fail Criteria

**Pass:** Both empty and whitespace-only queries are rejected before any ADO call, with a clear error.
**Fail:** Either case reaches ADO, returns an unclear/generic error, or silently returns an empty result set instead of erroring.
