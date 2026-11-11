---
id: ELITEA-4678
title: "Public API Context Strategy and Context Analytics Endpoints Remain Backward Compatible"
priority: critical
type: integration
module: context-management
status: draft
execution_type: manual
regression: true
tags: [feat:context-management, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6898]
---

## Preconditions

- Access to the public API or CLI with valid credentials for a test conversation
- A conversation exists that can be targeted via `PUT context_strategy` and `GET context_analytics`

## Test Data

| Field | Value |
|-------|-------|
| Endpoint | `PUT /elitea_core/context_strategy/prompt_lib/{projectId}/{conversationId}` |
| Endpoint | `GET /elitea_core/context_analytics/prompt_lib/{projectId}/{conversationId}` |
| Payload | `{ "max_context_tokens": <value> }` (no `context_window_mode`) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Call `PUT context_strategy` for the test conversation, sending only `context_window_mode` with no `max_context_tokens`. | The call succeeds (HTTP 2xx), is not rejected for missing the new field. |
| 2 | Call `PUT context_strategy` for the test conversation, sending only `max_context_tokens` with no `context_window_mode`. | The call succeeds (HTTP 2xx), is not rejected for missing the new field. |
| 3 | Inspect the resulting effective budget for the conversation (via the UI or a subsequent `GET context_analytics` call). | The legacy value is treated as a deprecated legacy request and capped at the usable input of the currently selected model. |
| 4 | Call `GET context_analytics` for the same conversation. | The response includes `max_tokens` and `utilization` fields in addition to the new fields (`window_mode`, `effective_window`, etc.). |

## Expected Final State

Public API clients that still send only the legacy `max_context_tokens` field continue to work without errors, and `GET context_analytics` remains backward compatible for consumers that only read the old fields.

## Pass/Fail Criteria

**Pass:**
- `PUT context_strategy` with only `max_context_tokens` succeeds
- The resulting budget is capped at the usable input of the model, not applied as a raw unbounded value
- `GET context_analytics` still returns `max_tokens` and `utilization`

**Fail:**
- The legacy-only payload is rejected by `PUT context_strategy`
- `GET context_analytics` omits `max_tokens` or `utilization`, breaking old clients
