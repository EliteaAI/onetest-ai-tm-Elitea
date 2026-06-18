---
id: ELITEA-0604
title: "Non-owner cannot access or send messages to another user's support conversation"
priority: high
type: functional
module: elitea-chat-bot
status: ready
execution_type: manual
tags: [conversation-ownership, authorization, story:4781, r-2.0.3, 403]
requirements: [4781, 4773]
---
# ELITEA-0604: Non-owner cannot access or send messages to another user's support conversation

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Verify that a user cannot access or send messages to a support conversation owned by another user. Attempting to GET or POST to another user's conversation UUID must return 403 Forbidden — not 200 or 404 with data.

## Preconditions

User-A has created a support conversation with known UUID.
User-B Bearer token is available.

## Test Data

User-A's conversation UUID
User-B Bearer token

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | As User-B, send GET /v2/support_assistant/conversations/{User-A-UUID} | HTTP 403 Forbidden or 404 Not Found — NOT 200 with User-A's conversation data |
| 2 | As User-B, send POST /v2/support_assistant/conversations/{User-A-UUID}/messages with any text | HTTP 403 Forbidden |
| 3 | As User-A (the owner), send GET /v2/support_assistant/conversations/{User-A-UUID} | HTTP 200 with correct conversation data |

## Expected Final State

HTTP 200 with correct conversation data

## Pass/Fail Criteria

PASS: Non-owner gets 403 or 404 on both GET and POST; owner gets 200.
FAIL: Non-owner receives 200 with conversation data; POST sends a message to another user's conversation.
