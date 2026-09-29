---
id: ELITEA-3451
title: "API Rejects Restrict Access Request from Non-Author"
priority: critical
type: functional
module: conversations
status: ready
execution_type: manual
tags: [feat:chat, access-control, restrict-access, api, permission, security, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6283]
---
# ELITEA-3451: API Rejects Restrict Access Request from Non-Author

**Module:** Conversations · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the server-side API rejects restrict access requests from users who are not the conversation author.

## Preconditions

- A public conversation exists created by User A
- User B is a project member (NOT the author)
- Valid API access token for User B

## Test Data

| Field | Value |
|-------|-------|
| User A | Conversation Author |
| User B | Project member, NOT author |
| API Endpoint | /api/conversations/{id}/restrict |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Authenticate as User B (non-author) | Token obtained for User B |
| 2 | Construct API request to restrict conversation access | Request body with valid participant list |
| 3 | Send request using User B's token | Server responds |
| 4 | Verify response status | HTTP 403 Forbidden |
| 5 | Verify error message | Message indicates only author can restrict access |
| 6 | Check conversation state | Access state UNCHANGED |
| 7 | Verify all current participants still have access | Access preserved |
| 8 | Authenticate as User A (author) | Token obtained for User A |
| 9 | Send same request using User A's token | Server ACCEPTS, operation succeeds |

## Expected Final State

- Only author's requests are processed
- Non-author attempts are rejected with 403
- Access state unchanged by unauthorized requests

## Teardown

- Restore conversation state if modified
