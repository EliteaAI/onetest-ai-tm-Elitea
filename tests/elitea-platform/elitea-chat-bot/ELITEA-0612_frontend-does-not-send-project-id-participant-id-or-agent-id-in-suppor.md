---
id: ELITEA-0612
title: "Frontend does not send project_id, participant_id, or agent_id in support API requests"
priority: high
type: functional
module: elitea-chat-bot
status: ready
execution_type: manual
tags: [no-hardcoded-ids, backend-driven, api-validation, story:4776, r-2.0.3]
requirements: [4776, 4781]
---
# ELITEA-0612: Frontend does not send project_id, participant_id, or agent_id in support API requests

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Verify that the Support Assistant frontend does not include project_id, participant_id, or agent_id in its API requests to the support endpoints. These values must be resolved server-side. Hardcoded IDs in FE requests are a security and maintainability defect — they would allow unauthorized project/agent targeting.

## Preconditions

Support Assistant is enabled.
Browser DevTools (Network tab) is available.
Tester knows the support API endpoint path (e.g., /v2/support_assistant/conversations).

## Test Data

Any test message

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Browser DevTools → Network tab; filter for "/support_assistant" | Network filter active |
| 2 | Open Support Assistant and send any message | A POST request to the conversations or messages endpoint is captured |
| 3 | Inspect the request body of the POST to the conversation creation endpoint | Request body does NOT contain project_id, participant_id, or agent_id fields |
| 4 | Inspect the request body of the POST to the message send endpoint | Request body does NOT contain agent_id or participant_id |
| 5 | Inspect the response body | The response includes conversation/message data that was created successfully |

## Expected Final State

The response includes conversation/message data that was created successfully

## Pass/Fail Criteria

PASS: None of the restricted fields appear in any request body from the frontend.
FAIL: Any of project_id, participant_id, or agent_id found in a request body sent by the frontend.
