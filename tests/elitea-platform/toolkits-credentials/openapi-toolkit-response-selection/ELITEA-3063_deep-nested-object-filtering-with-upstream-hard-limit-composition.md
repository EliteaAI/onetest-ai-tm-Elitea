---
id: ELITEA-3063
title: "Deep-Nested Object Filtering Works Correctly, Including Composition With an Upstream Hard Limit"
priority: medium
type: functional
module: openapi-toolkit-response-selection
status: draft
execution_type: manual
tags: [feat:toolkits, int:openapi, issue:6105, api, new]
requirements: [EliteaAI/elitea_issues#6105]
---

# ELITEA-3063: Deep-Nested Object Filtering Works, Including Composition With an Upstream Hard Limit

**Module:** Toolkits & Credentials / OpenAPI Toolkit Response Selection · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm collection discovery and filtering work correctly against a deeply nested JSON object response (not just a top-level flat array), and that this composes gracefully when the upstream API itself enforces a hard limit (observed live: an upstream `403` when exceeding a certain size, gracefully handled by retrying/composing at the upstream's allowed limit of 100). Confirmed live during manual exploration ("REST Countries" — deep nesting, upstream 403 limit — nested-object filtering + graceful upstream-limit handling).

---

## Preconditions

- An OpenAPI toolkit configured against an operation returning deeply nested JSON objects (e.g. a public countries/geo API), where requesting beyond a certain size triggers an upstream `403`/rate-limit response.

---

## Test Data

| Field | Value |
|-------|-------|
| `response_search` | a term matching nested fields several levels deep |
| Upstream constraint | API returns `403` above ~100 records in one call |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call the tool with `response_search` against the deeply nested dataset. | Call succeeds; matches are found correctly even though the matching field is nested several levels deep. |
| 2 | Observe how the tool/toolkit handles the upstream's hard limit (e.g. via its own retry/composition logic, separate from `response_limit`). | The upstream constraint is handled gracefully (e.g. capped at the upstream's allowed size) — no unhandled `403` bubbling up as an opaque failure. |
| 3 | Confirm the returned collection still reflects correct filtering despite the upstream-imposed data ceiling. | Filtering/ranking operates correctly on whatever data was successfully retrieved from upstream. |

---

## Expected Final State

Nested-object discovery/filtering is robust, and upstream-side hard limits are surfaced/handled gracefully rather than causing an unclear failure.

---

## Pass/Fail Criteria

**Pass:** Nested fields are correctly discovered/matched, and the upstream 403/limit condition is handled gracefully.
**Fail:** Nested matches are missed, or the upstream limit causes an unhandled error / unclear failure to the caller.
