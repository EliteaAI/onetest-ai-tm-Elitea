---
id: ELITEA-0236
title: "Agent invocation via Chat conversation API is logged in Analysis tab"
priority: high
type: functional
module: analysis-tab-activity-logging
status: ready
execution_type: manual
tags: [feat:analytics, issue:4007, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#4007]
---
# ELITEA-0236: Agent invocation via Chat conversation API is logged in Analysis tab

**Module:** Analysis Tab Activity Logging · **Priority:** High · **Type:** Functional

**Objective:** Verify that programmatic calls to the Chat conversation API that invoke an Agent are captured in the Analysis tab — covering the Chat API invocation surface.

**Coverage:**
- Chat API-originated agent call produces an Analysis tab log entry
- API invocation via the Chat endpoint is treated the same as Chat UI invocation for logging purposes
- Entry completeness comparable to Chat UI entries

## Preconditions

- Logged in to {{base_url}}
- A published Agent exists and is accessible via a Chat conversation
- Valid Bearer API token obtained from Platform Settings → API Keys
- A Chat conversation with the target Agent as participant exists (or can be created via API)
- HTTP client available (Postman, curl, or equivalent)

## Test Data

- Base URL: `{{base_url}}`
- Endpoint: Chat messages API (e.g., `POST /api/v2/conversations/{conversation_id}/messages`)
- Payload: `{"message": "Chat API invocation — analysis tab test"}`
- Header: `Authorization: Bearer {token}`
- `conversation_id`: ID of a conversation that has the target Agent as participant

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create or identify a Chat conversation that includes the target Agent as a participant. Note the `conversation_id`. | Conversation ID is available and the agent is confirmed as a participant. |
| 2 | Send POST to the Chat messages endpoint with payload `{"message": "Chat API invocation — analysis tab test"}` and Bearer token header. | HTTP 200 response. Agent response returned in the response body. |
| 3 | Navigate to the Analysis tab from the Platform sidebar. | Analysis tab opens with the activity log. |
| 4 | Locate the entry for the API-triggered chat message (filter by timestamp or agent name). | Entry is present with correct agent name, timestamp within 60 seconds, and Chat API source. |

## Expected Final State

Entry is present with correct agent name, timestamp within 60 seconds, and Chat API source.

## Pass/Fail Criteria

**Pass:**
- Chat API call produces an Analysis tab entry
- Entry is as complete as a Chat UI entry (agent name, timestamp present)

**Fail:**
- No entry for the Chat API call
- Chat API calls silently excluded from Analysis tab logging
