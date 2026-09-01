---
id: ELITEA-3047
title: "Baseline: No response_search/response_limit Supplied Returns the Unmodified Legacy Response"
priority: critical
type: functional
module: openapi-toolkit-response-selection
status: draft
execution_type: manual
tags: [feat:toolkits, int:openapi, issue:6105, api, new, regression]
requirements: [EliteaAI/elitea_issues#6105]
---

# ELITEA-3047: Baseline — No Selection Args Returns the Unmodified Legacy Response

**Module:** Toolkits & Credentials / OpenAPI Toolkit Response Selection · **Priority:** Critical · **Type:** Functional

**Objective:** Confirm the backward-compatibility guarantee: calling an OpenAPI toolkit operation with neither `response_search` nor `response_limit` supplied returns the response exactly as before this feature existed — no `_elitea_response_selection` wrapper, no altered structure. Confirmed live during manual exploration (raw passthrough confirmed) against a flat-array API.

---

## Preconditions

- An OpenAPI toolkit configured against an operation returning a JSON array/collection (e.g. a public REST API such as GitHub Search API or similar).

---

## Test Data

| Field | Value |
|-------|-------|
| `response_search` | not supplied |
| `response_limit` | not supplied |
| `regexp` | not supplied |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call the tool with no selection arguments and no `regexp`. | Call succeeds. |
| 2 | Inspect the returned JSON. | Response is byte-for-byte the same shape/content as the raw upstream response — no `_elitea_response_selection` key present anywhere. |

---

## Expected Final State

The tool's output is unaffected by this feature when neither new argument is used.

---

## Pass/Fail Criteria

**Pass:** Output matches the raw upstream response exactly; no selection metadata is injected.
**Fail:** Any structural change, wrapper, or metadata appears despite no selection arguments being passed.
