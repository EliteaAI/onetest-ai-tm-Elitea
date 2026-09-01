---
id: ELITEA-3061
title: "regexp Combined With response_search or response_limit Raises incompatible_response_controls"
priority: critical
type: functional
module: openapi-toolkit-response-selection
status: draft
execution_type: manual
tags: [feat:toolkits, int:openapi, issue:6105, api, new]
requirements: [EliteaAI/elitea_issues#6105]
---

# ELITEA-3061: regexp Combined With Selection Args Raises incompatible_response_controls

**Module:** Toolkits & Credentials / OpenAPI Toolkit Response Selection · **Priority:** Critical · **Type:** Functional

**Objective:** Confirm supplying `regexp` together with `response_search` and/or `response_limit` on the same call is rejected with a hard validation error (`incompatible_response_controls`: "'regexp' cannot be combined with 'response_search' or 'response_limit'. Use structured response selection without regexp to keep JSON output valid.") rather than attempting to apply both and risking invalid JSON. Confirmed live during manual exploration ("regexp + response_search conflict" — hard validation error).

---

## Preconditions

- An OpenAPI toolkit operation with a working `regexp` pattern and a searchable JSON response.

---

## Test Data

| Field | Value |
|-------|-------|
| `regexp` | any valid pattern |
| `response_search` | any valid query |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call the tool with both `regexp` and `response_search` set. | Call is rejected with error code `incompatible_response_controls` and the documented message. |
| 2 | Call the tool with `regexp` and `response_limit` set (no `response_search`). | Same rejection with `incompatible_response_controls`. |

---

## Expected Final State

`regexp` and the new selection args are mutually exclusive, enforced with a clear, specific error code.

---

## Pass/Fail Criteria

**Pass:** Both combinations are rejected with the exact `incompatible_response_controls` error.
**Fail:** Either combination is silently accepted, applies both mechanisms, or returns a generic/unclear error instead.
