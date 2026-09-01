---
id: ELITEA-3071
title: "response_search and response_limit Are Never Forwarded to the Target API as Real Request Params"
priority: high
type: functional
module: openapi-toolkit-response-selection
status: draft
execution_type: manual
tags: [feat:toolkits, int:openapi, issue:6105, api, security]
requirements: [EliteaAI/elitea_issues#6105]
---

# ELITEA-3071: response_search and response_limit Are Never Forwarded to the Target API

**Module:** Toolkits & Credentials / OpenAPI Toolkit Response Selection · **Priority:** High · **Type:** Functional

**Objective:** Confirm `response_search` and `response_limit` are popped from the tool's kwargs before the real upstream HTTP call is made, and never appear as query params, path params, headers, or body fields sent to the target API. This must hold even for operations that happen to declare a same-named legitimate parameter, and even when the upstream API would otherwise silently accept/ignore unexpected params (making a leak easy to miss without directly inspecting the outgoing request).

---

## Preconditions

- Ability to inspect the actual outgoing HTTP request made by the toolkit (e.g. via a request-echoing endpoint like httpbin, or network capture/logging).

---

## Test Data

| Field | Value |
|-------|-------|
| Endpoint | a request-echoing endpoint (e.g. httpbin `/get`) or an endpoint with request logging visibility |
| `response_search` | `"test query"` |
| `response_limit` | `5` |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call the tool against the echoing endpoint with both `response_search` and `response_limit` set. | Call succeeds; `_elitea_response_selection` metadata confirms selection was applied locally. |
| 2 | Inspect the actual outgoing request (query string, headers, body) via the echo response or captured request. | Neither `response_search` nor `response_limit` (nor their values) appear anywhere in the outgoing request. |
| 3 | Repeat against an operation whose real declared parameters happen to include a same-named or similarly-named field, if available. | The real declared parameter is unaffected/forwarded correctly if explicitly supplied separately; the selection args are still stripped and never conflated with it. |

---

## Expected Final State

Selection-control arguments remain purely local to response post-processing and never leak into the actual API request.

---

## Pass/Fail Criteria

**Pass:** No trace of `response_search`/`response_limit` in the outgoing request in any case.
**Fail:** Either value appears anywhere in the actual outgoing HTTP request.

---

## Notes

Carried over unmodified from the original #6105 checklist (not re-verified via a fresh live request this session, but confirmed correct by source-code review of PR #556 — the args are popped from kwargs prior to the HTTP call).
