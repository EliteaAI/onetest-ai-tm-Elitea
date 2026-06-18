---
id: ELITEA-0605
title: "POST message to a support conversation returns assistant response and maintains context"
priority: high
type: functional
module: elitea-chat-bot
status: ready
execution_type: manual
tags: [message-api, story:4781, multi-turn, context, r-2.0.3]
requirements: [4781, 4775]
---
# ELITEA-0605: POST message to a support conversation returns assistant response and maintains context

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Verify the message endpoint POST /v2/support_assistant/conversations/{uuid}/messages returns a valid assistant response for the first message. A second message in the same conversation uses context from the first message in generating the response.

## Preconditions

A support conversation has been created (use POST /v2/support_assistant/conversations first).
Authenticated user Bearer token available.

## Test Data

Conversation UUID from setup
Message 1 body: { "text": "My username is APITestUser." }
Message 2 body: { "text": "What username did I just give you?" }

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Send POST /v2/support_assistant/conversations/{uuid}/messages with message 1 body | HTTP 200; response contains an assistant_message or equivalent field with content |
| 2 | Inspect the response | Assistant response is a non-empty string; no error fields |
| 3 | Send message 2 in the same conversation ({uuid}) | HTTP 200; response is received |
| 4 | Inspect the response to message 2 | Response references "APITestUser" — context from message 1 is preserved |

## Expected Final State

Response references "APITestUser" — context from message 1 is preserved

## Pass/Fail Criteria

PASS: Both return 200 with non-empty responses; message 2 response references context from message 1.
FAIL: 4xx or 5xx on either message; message 2 response is context-free (treats it as a fresh request).
