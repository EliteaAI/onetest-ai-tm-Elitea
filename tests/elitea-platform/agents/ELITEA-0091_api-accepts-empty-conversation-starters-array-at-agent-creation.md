---
id: ELITEA-0091
title: "API accepts empty conversation_starters array at agent creation"
priority: medium
type: functional
module: agents
status: ready
execution_type: manual
tags: [rca:missing-functionality, rca:data-quality, nfr:validation, feat:agents, eng:backend, eng:api, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4933]
---
# ELITEA-0091: API accepts empty conversation_starters array at agent creation

**Module:** Agents · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that an empty `conversation_starters` array `[]` is treated as a valid value — accepted by the API, persisted correctly, and rendered gracefully in the UI without a crash.

**Coverage:**
- Empty array `[]` returns 201 Created (not incorrectly rejected by the new validation)
- `conversation_starters` is stored as `[]` in the database
- Agent detail view opens without any crash or console error
- Conversation Starters section shows an empty or default state — not a crash

## Preconditions

- User is authenticated with a valid session token
- Environment: {{base_url}}
- API client is configured and connected
- A valid `project_id` is known
- User is also logged in to the UI at {{base_url}} for the UI step

## Test Data

**Endpoint:** `POST /api/v2/elitea_core/applications/prompt_lib/{project_id}`

**Request payload:**
```json
{
  "name": "TC-CS-Empty-Array",
  "description": "Edge case: empty conversation_starters array",
  "type": "interface",
  "webhook_secret": null,
  "versions": [
    {
      "name": "base",
      "tags": [],
      "instructions": "",
      "variables": [],
      "tools": [],
      "llm_settings": {
        "max_tokens": -1,
        "temperature": 0.6,
        "reasoning_effort": "medium",
        "model_name": "gpt-5.2",
        "model_project_id": 1
      },
      "conversation_starters": [],
      "agent_type": "openai",
      "welcome_message": "",
      "meta": {
        "step_limit": 25
      }
    }
  ]
}
```
Expected `conversation_starters` in response: `[]`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Send POST to `/api/v2/elitea_core/applications/prompt_lib/{project_id}` with the payload above where `conversation_starters` is an empty array `[]`. | Request is sent successfully. |
| 2 | Observe the HTTP response status code. | HTTP 201 Created (or 200 OK). No validation error is returned — empty array is a valid value. |
| 3 | Inspect the response body — check the `conversation_starters` field. | `conversation_starters` is `[]` in the response. No null or unexpected values injected. |
| 4 | Navigate in the UI to the Agents section and open the newly created agent 'TC-CS-Empty-Array'. | Agent detail view opens without any crash or console error. The Conversation Starters section shows an empty state or a placeholder prompt — the page is fully interactive. |

## Expected Final State

Agent detail view opens without any crash or console error. The Conversation Starters section shows an empty state or a placeholder prompt — the page is fully interactive.

## Pass/Fail Criteria

**Pass:**
- API returns 201 Created for an empty `conversation_starters` array
- `conversation_starters` is stored and returned as `[]`
- Agent opens in the UI without any crash or console error

**Fail:**
- API returns 400 for an empty array (over-validation: the fix incorrectly rejects `[]`)
- UI crashes when rendering an agent with no conversation starters
