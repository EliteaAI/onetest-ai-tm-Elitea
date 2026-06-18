---
id: ELITEA-0608
title: "PUT /v2/support_assistant/config by Platform Admin updates configuration"
priority: high
type: functional
module: elitea-chat-bot
status: draft
execution_type: manual
tags: [put-config, story:4781, config-api, admin-only, r-2.0.3]
requirements: [4781, 4776]
---
# ELITEA-0608: PUT /v2/support_assistant/config by Platform Admin updates configuration

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Verify that the PUT /v2/support_assistant/config endpoint allows a Platform Admin to update the Support Assistant configuration (toggle, active agent). Also verify that a regular user receives 403 Forbidden when attempting the same call.

## Preconditions

Platform Admin Bearer token and regular user Bearer token both available.
API client configured.

## Test Data

Admin token: valid Platform Admin Bearer token
User token: valid regular user Bearer token
Payload: { "enabled": true, "agent_id": "<valid-agent-id>" } (adjust to actual schema)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Send PUT /v2/support_assistant/config with admin Bearer token and a valid payload | HTTP 200 response; response body confirms updated config |
| 2 | Send GET /v2/support_assistant/config to confirm the change | GET response reflects the updated values from step 1 |
| 3 | Send PUT /v2/support_assistant/config with a regular user Bearer token (same payload) | HTTP 403 Forbidden response |
| 4 | Send PUT /v2/support_assistant/config with no Bearer token | HTTP 401 Unauthorized response |

## Expected Final State

HTTP 401 Unauthorized response

## Pass/Fail Criteria

PASS: Admin PUT returns 200 and config is updated; regular user gets 403; no auth gets 401.
FAIL: Regular user receives 200; admin PUT returns error; config not updated after successful PUT.
