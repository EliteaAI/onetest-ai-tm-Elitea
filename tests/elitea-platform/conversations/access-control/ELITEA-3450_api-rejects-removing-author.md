---
id: ELITEA-3450
title: "API Rejects Removing the Owner from Chat Access"
priority: critical
type: functional
module: conversations
status: ready
execution_type: manual
tags: [feat:chat, access-control, share-chat, api, security, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6283, EliteaAI/elitea_issues#7489]
---
# ELITEA-3450: API Rejects Removing the Owner from Chat Access

**Module:** Conversations · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the server-side API rejects any attempt to save the chat access (Share Chat > Team) without the owner, so the owner always keeps access.

## Preconditions

- Valid API access token for the conversation author
- A conversation owned by the author exists in a team project, with known ID
- API testing tool available (Postman, curl, browser dev tools)

## Test Data

| Field | Value |
|-------|-------|
| API Endpoint | Access request sent by Share Chat > Team > Save (captured in DevTools) |
| Auth | Valid author token |
| Method | PUT/POST |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As the owner, open Share > Team, add a user, click Save; capture the access request in DevTools > Network | Endpoint and payload are recorded |
| 2 | Replay the request with a payload without the owner (empty list, then only other users) | Server responds |
| 3 | Verify the response | Rejected (400/422); the message says the owner must keep access |
| 4 | Reopen Share > Team | The owner is listed with the badge "Owner"; the list is unchanged |
| 5 | Replay the request with a payload that includes the owner | Request is accepted |

## Expected Final State

- API properly validates author inclusion
- Conversation always has author access
- Cannot bypass author requirement via API

## Teardown

- Restore original conversation state if modified
