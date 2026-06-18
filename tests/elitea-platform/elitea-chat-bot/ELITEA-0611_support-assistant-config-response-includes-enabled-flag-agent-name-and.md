---
id: ELITEA-0611
title: "Support Assistant config response includes enabled flag, agent name, and avatar"
priority: high
type: functional
module: elitea-chat-bot
status: ready
execution_type: manual
tags: [backend-driven, config-api, story:4776, branding, r-2.0.3]
requirements: [4776, 4781]
---
# ELITEA-0611: Support Assistant config response includes enabled flag, agent name, and avatar

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Verify that the GET /v2/support_assistant/config endpoint returns a valid response including at least the enabled flag, the configured assistant name, and the avatar/icon reference when the Support Assistant is enabled. This confirms that the frontend receives all branding and activation data from a single config call — no hardcoded values needed.

## Preconditions

Support Assistant is enabled in Admin → Guardrails.
Tester has authenticated API access (valid Bearer token for a regular user).

## Test Data

Authenticated HTTP client (Postman or curl)
Endpoint: GET /v2/support_assistant/config

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Send GET /v2/support_assistant/config with a valid regular user Bearer token | HTTP 200 response |
| 2 | Inspect the response body | Response includes enabled: true (or equivalent field) |
| 3 | Check for the assistant name field | Response includes an agent_name or name field with a non-empty string value |
| 4 | Check for the avatar/icon field | Response includes an avatar_url or icon field |
| 5 | As admin, disable the Support Assistant; re-send the same request | Response still returns HTTP 200 but with enabled: false |
| 6 | As admin, re-enable; confirm enabled: true is returned again | Config reflects the current toggle state |

## Expected Final State

Config reflects the current toggle state

## Pass/Fail Criteria

PASS: 200 response with enabled, name, and avatar fields; enabled flag changes with admin toggle.
FAIL: 4xx or 5xx response; missing fields; enabled field doesn't reflect current admin state.
