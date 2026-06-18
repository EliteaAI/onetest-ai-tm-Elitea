---
id: ELITEA-0090
title: "API rejects non-string values in conversation_starters at agent creation [Parametrized]"
priority: critical
type: functional
module: agents
status: ready
execution_type: manual
tags: [rca:missing-functionality, rca:data-quality, nfr:validation, feat:agents, eng:backend, eng:api, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4933]
---
# ELITEA-0090: API rejects non-string values in conversation_starters at agent creation [Parametrized]

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the agent creation API endpoint rejects any payload where `conversation_starters` contains non-string items, returning a 400 Bad Request with a descriptive validation error and persisting no data.

**Coverage:**
- Null value `[null]` is rejected
- Integer value `[42]` is rejected
- Empty object `[{}]` is rejected
- Boolean value `[true]` is rejected
- Mixed array `[null, 42, {}, "valid starter"]` is rejected even when one item is a valid string

## Preconditions

- User is authenticated with a valid session token
- Environment: {{base_url}}
- API client (e.g. Postman, curl, or an SDK) is configured and connected to the environment
- A valid `project_id` is known (obtainable from the project URL or project settings)
- No pre-existing agent with the test name exists in the project

## Test Data

**Endpoint:** `POST /api/v2/elitea_core/applications/prompt_lib/{project_id}`

**Base payload template** (substitute `conversation_starters` per variant):
```json
{
  "name": "TC-CS-Invalid-{variant}",
  "description": "desc",
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

| Variant | conversation_starters value | Description |
|---------|----------------------------|-------------|
| A | `[null]` | Null only |
| B | `[42]` | Integer only |
| C | `[{}]` | Empty object only |
| D | `[true]` | Boolean only |
| E | `[null, 42, {}, "valid starter"]` | Mixed — exact bug report payload |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | For Variant A: send POST to `/api/v2/elitea_core/applications/prompt_lib/{project_id}` with the base payload template and `"conversation_starters": [null]`. | HTTP 400 Bad Request is returned. Response body contains a validation error referencing the `conversation_starters` field. |
| 2 | For Variant B: repeat the POST with `"conversation_starters": [42]`. | HTTP 400 Bad Request. Validation error states integer values are not allowed in `conversation_starters`. |
| 3 | For Variant C: repeat the POST with `"conversation_starters": [{}]`. | HTTP 400 Bad Request. Validation error states object values are not allowed. |
| 4 | For Variant D: repeat the POST with `"conversation_starters": [true]`. | HTTP 400 Bad Request. Validation error states boolean values are not allowed. |
| 5 | For Variant E (exact bug payload): repeat the POST with `"conversation_starters": [null, 42, {}, "valid starter"]`. | HTTP 400 Bad Request. Presence of one valid string does NOT cause the request to pass. Validation error is returned for the non-string items. |
| 6 | After all variants, query the agents list via GET `/api/v2/elitea_core/applications/prompt_lib/{project_id}` and search for any agent named `TC-CS-Invalid-*`. | No agent matching any test variant name exists. No data was persisted for any variant. |

## Expected Final State

No agent matching any test variant name exists. No data was persisted for any variant.

## Pass/Fail Criteria

**Pass:**
- All 5 variants return HTTP 400 Bad Request
- Each response body contains a descriptive validation error referencing `conversation_starters`
- No agent is created or persisted in the system for any variant

**Fail:**
- Any variant returns HTTP 2xx and the agent is created
- Non-string values are stored in the database
- Variant E passes because `"valid starter"` is present alongside invalid items
