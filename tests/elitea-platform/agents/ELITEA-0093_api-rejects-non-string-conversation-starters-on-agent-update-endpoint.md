---
id: ELITEA-0093
title: "API rejects non-string conversation_starters on agent update endpoint [Parametrized]"
priority: high
type: functional
module: agents
status: ready
execution_type: manual
tags: [rca:missing-functionality, rca:data-quality, nfr:validation, feat:agents, eng:backend, eng:api, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4933]
---
# ELITEA-0093: API rejects non-string conversation_starters on agent update endpoint [Parametrized]

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that the same `conversation_starters` type validation enforced at agent creation is also applied on the agent update (PUT/PATCH) endpoint — preventing malformed values from overwriting previously valid data.

**Coverage:**
- Null-only update payload `[null]` is rejected with 400
- Integer-only update payload `[42]` is rejected with 400
- Mixed invalid update payload `[null, 42, {}]` is rejected with 400
- Original valid `conversation_starters` remain unchanged in the database after each rejection

## Preconditions

- A valid agent exists in the system with `conversation_starters: ["How can you help me?", "Summarize this document", "What are your capabilities?"]` — created via TC-3 (TC-CS-Valid-Strings) or equivalent
- The agent's `id` and `project_id` are known
- User is authenticated with a valid session token
- API client is configured and connected to {{base_url}}

## Test Data

**Endpoint:** `PUT /api/v2/elitea_core/applications/prompt_lib/{project_id}/{agent_id}` (or PATCH equivalent)

**Base update payload template** (substitute `conversation_starters` per variant):
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
      "conversation_starters": <VARIANT_VALUE>,
      "agent_type": "openai",
      "welcome_message": "",
      "meta": {
        "step_limit": 25
      }
    }
  ]
}
```

**Parameter table:**

| Variant | conversation_starters value |
|---------|-----------------------------|
| A | `[null]` |
| B | `[42]` |
| C | `[null, 42, {}]` |

**Original valid value (for verification):** `["How can you help me?", "Summarize this document", "What are your capabilities?"]`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | For Variant A: send PUT/PATCH to the agent update endpoint for agent 'TC-CS-Valid-Strings' with `"conversation_starters": [null]`. | HTTP 400 Bad Request is returned. Validation error references `conversation_starters`. |
| 2 | For Variant B: repeat the PUT/PATCH with `"conversation_starters": [42]`. | HTTP 400 Bad Request. Validation error states integer values are not allowed. |
| 3 | For Variant C: repeat the PUT/PATCH with `"conversation_starters": [null, 42, {}]`. | HTTP 400 Bad Request. All non-string items are flagged. |
| 4 | After all three variants, send GET to `/api/v2/elitea_core/applications/prompt_lib/{project_id}/{agent_id}` to retrieve the current agent state. | `conversation_starters` still equals `["How can you help me?", "Summarize this document", "What are your capabilities?"]`. No variant overwrote the original data. |

## Expected Final State

`conversation_starters` still equals `["How can you help me?", "Summarize this document", "What are your capabilities?"]`. No variant overwrote the original data.

## Pass/Fail Criteria

**Pass:**
- All three variants return HTTP 400 Bad Request with a descriptive validation error
- The original valid `conversation_starters` are unchanged after all rejected update attempts

**Fail:**
- Any variant is accepted with 2xx and malformed values overwrite the valid data
- Validation is applied at creation but skipped on the update endpoint
