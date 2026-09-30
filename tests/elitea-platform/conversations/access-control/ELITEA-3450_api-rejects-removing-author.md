---
id: ELITEA-3450
title: "API Rejects Removing Author from Conversation"
priority: critical
type: functional
module: conversations
status: ready
execution_type: manual
tags: [feat:chat, access-control, restrict-access, api, security, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6283]
---
# ELITEA-3450: API Rejects Removing Author from Conversation

**Module:** Conversations · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the server-side API rejects any attempt to restrict a conversation without including the author in the participant list.

## Preconditions

- Valid API access token for the conversation author
- A public conversation exists with known ID
- API testing tool available (Postman, curl, browser dev tools)

## Test Data

| Field | Value |
|-------|-------|
| API Endpoint | /api/conversations/{id}/restrict |
| Auth | Valid author token |
| Method | PUT/POST |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Construct API request to restrict conversation access | Request body prepared |
| 2 | Set participant list to empty array `[]` | Payload: `{"participants": []}` |
| 3 | Send PUT/POST request to restrict access endpoint | Server responds |
| 4 | Verify response status | HTTP 400 Bad Request or 422 Unprocessable Entity |
| 5 | Verify error message | Message indicates author/creator must be included |
| 6 | Check conversation state via GET request | Access state UNCHANGED |
| 7 | Verify author still has access | Author can still open conversation |
| 8 | Try with list excluding only author | Include other users but not author |
| 9 | Send request | Server REJECTS with same error |
| 10 | Try with list including author | Include author + others |
| 11 | Send request | Server ACCEPTS, operation succeeds |

## Expected Final State

- API properly validates author inclusion
- Conversation always has author access
- Cannot bypass author requirement via API

## Teardown

- Restore original conversation state if modified
