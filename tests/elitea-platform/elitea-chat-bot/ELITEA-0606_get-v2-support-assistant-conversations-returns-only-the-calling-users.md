---
id: ELITEA-0606
title: "GET /v2/support_assistant/conversations returns only the calling user's conversations"
priority: critical
type: functional
module: elitea-chat-bot
status: ready
execution_type: manual
tags: [conversation-api, user-scoping, story:4781, r-2.0.3, privacy]
requirements: [4781, 4773]
---
# ELITEA-0606: GET /v2/support_assistant/conversations returns only the calling user's conversations

**Module:** Elitea Chat Bot · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the conversations listing endpoint for the support assistant returns only the conversations owned by the authenticated user. User-A's call must not include User-B's conversations in the response, even if both are in the same environment.

## Preconditions

Two authenticated regular user accounts: User-A and User-B.
Both have created support conversations (via UI or API).

## Test Data

User-A Bearer token
User-B Bearer token
Endpoint: GET /v2/support_assistant/conversations

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Send GET /v2/support_assistant/conversations with User-A token | HTTP 200; list contains User-A's conversations only |
| 2 | Note the conversation IDs returned for User-A | Record IDs |
| 3 | Send GET /v2/support_assistant/conversations with User-B token | HTTP 200; list contains User-B's conversations only |
| 4 | Verify no conversation IDs from User-A's list appear in User-B's response | No overlap in conversation IDs |
| 5 | Attempt GET /v2/support_assistant/conversations with no Bearer token | HTTP 401 Unauthorized |

## Expected Final State

HTTP 401 Unauthorized

## Pass/Fail Criteria

PASS: Each user sees only their own conversations; IDs do not overlap; 401 without auth.
FAIL: User-B's conversations appear in User-A's response; or vice versa; unauthenticated call returns data.
