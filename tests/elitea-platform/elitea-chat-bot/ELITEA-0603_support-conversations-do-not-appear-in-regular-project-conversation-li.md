---
id: ELITEA-0603
title: "Support conversations do not appear in regular project conversation listing"
priority: high
type: functional
module: elitea-chat-bot
status: ready
execution_type: manual
tags: [conversation-isolation, hidden-project, regular-api, story:4781, r-2.0.3]
requirements: [4781, 4773]
---
# ELITEA-0603: Support conversations do not appear in regular project conversation listing

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Verify that support conversations created via the Support Assistant API do not appear in the standard conversation listing endpoint (GET /v2/elitea_core/{project_id}/conversations). Support conversations must be isolated to the support API and the hidden project — not bleed into regular chat history.

## Preconditions

User has created at least one support conversation via the Support Assistant.
User knows their regular project ID.
Authenticated Bearer token available.

## Test Data

Regular project ID (from the user's main project)
Endpoint: GET /v2/elitea_core/{project_id}/conversations

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create a support conversation via POST /v2/support_assistant/conversations | Conversation created; note the returned UUID |
| 2 | Note the conversation UUID returned in step 1 | UUID recorded |
| 3 | Send GET /v2/elitea_core/{regular_project_id}/conversations with the same user token | HTTP 200; a list of regular conversations is returned |
| 4 | Search the response for the support conversation UUID noted in step 2 | The support conversation UUID does NOT appear in the regular project conversations list |
| 5 | Confirm the support conversation is accessible via the support API | GET /v2/support_assistant/conversations returns the conversation correctly |

## Expected Final State

GET /v2/support_assistant/conversations returns the conversation correctly

## Pass/Fail Criteria

PASS: Support conversation UUID absent from regular project listing; accessible via support API.
FAIL: Support conversation appears in the regular project conversation list.
