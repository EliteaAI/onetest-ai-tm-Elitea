---
id: ELITEA-0094
title: "API accepts valid string-only conversation_starters at agent creation (regression)"
priority: high
type: functional
module: agents
status: ready
execution_type: manual
tags: [rca:missing-functionality, rca:data-quality, nfr:validation, feat:agents, eng:backend, eng:api, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4933]
---
# ELITEA-0094: API accepts valid string-only conversation_starters at agent creation (regression)

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that the agent creation API continues to accept and persist a `conversation_starters` array containing only valid non-empty strings after the validation fix is applied — confirming no over-validation regression.

**Coverage:**
- All-string `conversation_starters` payload returns 201 Created
- All string values are persisted exactly as provided
- Created agent opens in the UI without errors
- Conversation starters are rendered correctly in the agent detail view

## Preconditions

- User is authenticated with a valid session token
- Environment: {{base_url}}
- API client is configured and connected
- A valid `project_id` is known
- User is also logged in to the UI at {{base_url}} for step 4

## Test Data

**Endpoint:** `POST /api/v2/elitea_core/applications/prompt_lib/{project_id}`

**Request payload:**
```json
{
  "name": "TC-CS-Valid-Strings",
  "description": "Regression test for valid conversation starters",
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
      "conversation_starters": [
        "How can you help me?",
        "Summarize this document",
        "What are your capabilities?"
      ],
      "agent_type": "openai",
      "welcome_message": "",
      "meta": {
        "step_limit": 25
      }
    }
  ]
}
```
Expected `conversation_starters` in response: `["How can you help me?", "Summarize this document", "What are your capabilities?"]`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Send POST to `/api/v2/elitea_core/applications/prompt_lib/{project_id}` with the payload above containing `conversation_starters` as an array of three valid strings. | Request is sent successfully. |
| 2 | Observe the HTTP response status code. | HTTP 201 Created (or 200 OK). No validation error is returned. |
| 3 | Inspect the response body — find the `conversation_starters` field in the returned agent object. | All three string values — 'How can you help me?', 'Summarize this document', 'What are your capabilities?' — are present and intact in the response. |
| 4 | Navigate in the UI to the Agents section and open the newly created agent 'TC-CS-Valid-Strings'. | Agent detail view opens without any crash or console error. The three conversation starters are displayed correctly in the Conversation Starters section. |

## Expected Final State

Agent detail view opens without any crash or console error. The three conversation starters are displayed correctly in the Conversation Starters section.

## Pass/Fail Criteria

**Pass:**
- API returns 201 Created for a valid all-string payload
- All three string values are persisted and returned in the response
- Agent opens in the UI with conversation starters rendered correctly

**Fail:**
- API returns 400 for a valid all-string payload (over-validation regression introduced by the fix)
- Any conversation starter value is missing, truncated, or corrupted in the response
