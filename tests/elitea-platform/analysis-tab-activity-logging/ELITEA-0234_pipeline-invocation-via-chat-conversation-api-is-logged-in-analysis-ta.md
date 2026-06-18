---
id: ELITEA-0234
title: "Pipeline invocation via Chat conversation API is logged in Analysis tab"
priority: high
type: functional
module: analysis-tab-activity-logging
status: ready
execution_type: manual
tags: [feat:analytics, issue:4007, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#4007]
---
# ELITEA-0234: Pipeline invocation via Chat conversation API is logged in Analysis tab

**Module:** Analysis Tab Activity Logging · **Priority:** High · **Type:** Functional

**Objective:** Verify that programmatic calls to the Chat conversation API that invoke a Pipeline are captured in the Analysis tab — covering the Chat API surface for pipelines.

**Coverage:**
- Chat API-triggered pipeline execution produces an Analysis tab log entry
- All programmatic pipeline invocation paths (predict API and Chat API) are logged
- Entry completeness comparable to UI-triggered pipeline entries

## Preconditions

- Logged in to {{base_url}}
- A published Pipeline exists and is accessible via a Chat conversation
- Valid Bearer API token obtained from Platform Settings → API Keys
- A Chat conversation with the target Pipeline as participant exists (or can be created via API)
- HTTP client available (Postman, curl, or equivalent)

## Test Data

- Base URL: `{{base_url}}`
- Endpoint: Chat messages API (e.g., `POST /api/v2/conversations/{conversation_id}/messages`)
- Payload: `{"message": "Chat API pipeline invocation — analysis tab test"}`
- Header: `Authorization: Bearer {token}`
- `conversation_id`: ID of a conversation that has the target Pipeline as participant

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create or identify a Chat conversation that includes the target Pipeline as a participant. Note the `conversation_id`. | Conversation ID is available and the pipeline is confirmed as a participant. |
| 2 | Send POST to the Chat messages endpoint with payload `{"message": "Chat API pipeline invocation — analysis tab test"}` and Bearer token header. | HTTP 200 response. Pipeline output returned in response body. |
| 3 | Navigate to the Analysis tab from the Platform sidebar. | Analysis tab opens with the activity log. |
| 4 | Locate the entry for the API-triggered pipeline invocation (filter by timestamp or pipeline name). | Entry is present with correct pipeline name, timestamp within 60 seconds, and Chat API source. |

## Expected Final State

Entry is present with correct pipeline name, timestamp within 60 seconds, and Chat API source.

## Pass/Fail Criteria

**Pass:**
- Chat API pipeline call produces an Analysis tab entry
- Entry is as complete as a UI-triggered entry

**Fail:**
- No entry for the Chat API pipeline invocation
- Pipeline Chat API calls silently excluded from Analysis tab logging
