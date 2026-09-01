---
id: ELITEA-3057
title: "response_limit Boundary Validation: 0/Negative/201 Rejected, 200 Accepted"
priority: high
type: functional
module: openapi-toolkit-response-selection
status: draft
execution_type: manual
tags: [feat:toolkits, int:openapi, issue:6105, api, new]
requirements: [EliteaAI/elitea_issues#6105]
---

# ELITEA-3057: response_limit Boundary Validation

**Module:** Toolkits & Credentials / OpenAPI Toolkit Response Selection · **Priority:** High · **Type:** Functional

**Objective:** Confirm `response_limit` enforces the documented 1–200 range: `0` and negative values are rejected with a validation error referencing the valid range; `201` is rejected referencing the 200 cap; `200` (the exact boundary) is accepted and returns up to 200 items. Confirmed live during the follow-up checklist pass ("response_limit boundary validation").

---

## Preconditions

- An OpenAPI toolkit configured against an operation returning at least 200 items, to distinguish "accepted but capped by data" from "accepted at the true boundary."

---

## Test Data

| Field | Value |
|-------|-------|
| Case A | `response_limit=0` |
| Case B | `response_limit=-1` |
| Case C | `response_limit=201` |
| Case D | `response_limit=200` |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call with `response_limit=0`. | Rejected with a validation error referencing the 1–200 valid range. |
| 2 | Call with `response_limit=-1`. | Rejected with the same 1–200 range validation error. |
| 3 | Call with `response_limit=201`. | Rejected with a validation error referencing the 200 cap. |
| 4 | Call with `response_limit=200`. | Accepted; up to 200 items returned (not rejected as "over" the boundary). See [[ELITEA-3058]] for a known anomaly observed at this exact boundary. |

---

## Expected Final State

`response_limit` validation correctly enforces an inclusive [1, 200] range.

---

## Pass/Fail Criteria

**Pass:** 0, -1, and 201 are all rejected with clear range-referencing errors; 200 is accepted.
**Fail:** Any out-of-range value is silently accepted/clamped, or the valid boundary (200) is incorrectly rejected.
