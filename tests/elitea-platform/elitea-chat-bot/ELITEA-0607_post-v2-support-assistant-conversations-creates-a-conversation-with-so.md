---
id: ELITEA-0607
title: "POST /v2/support_assistant/conversations creates a conversation with source=support and is_private=true"
priority: critical
type: functional
module: elitea-chat-bot
status: draft
execution_type: manual
tags: [conversation-api, source-support, story:4781, is-private, invariants, r-2.0.3]
requirements: [4781, 4773]
---
# ELITEA-0607: POST /v2/support_assistant/conversations creates a conversation with source=support and is_private=true

**Module:** Elitea Chat Bot · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that creating a support conversation via POST /v2/support_assistant/conversations always produces a conversation with source = 'support' and is_private = true in the response. These invariants must not be overridable by the frontend request body. This is both a correctness check and a privacy enforcement check.

## Preconditions

Support Assistant is enabled.
Authenticated regular user Bearer token available.
API client configured.

## Test Data

Regular user Bearer token
Endpoint: POST /v2/support_assistant/conversations
Request body: minimal (no project_id, no source override)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Send POST /v2/support_assistant/conversations with a regular user token and minimal body | HTTP 201 response; response body contains a conversation object |
| 2 | Inspect the source field in the response | source = "support" (or equivalent metadata field) |
| 3 | Inspect the is_private field in the response | is_private = true |
| 4 | Attempt to send the same request but with "source": "chat" in the request body | HTTP 201 still returns a conversation, but source in the response is still "support" (not "chat") — server enforces invariant |
| 5 | Attempt to send with "is_private": false in the request body | Response still has is_private: true — server ignores the override |

## Expected Final State

Response still has is_private: true — server ignores the override

## Pass/Fail Criteria

PASS: Both invariants enforced in all cases; client cannot override them.
FAIL: source or is_private can be set to non-support values by the client.
