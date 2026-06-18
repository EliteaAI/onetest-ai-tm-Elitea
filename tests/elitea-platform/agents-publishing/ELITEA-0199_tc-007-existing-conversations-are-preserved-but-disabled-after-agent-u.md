---
id: ELITEA-0199
title: "TC-007: Existing Conversations Are Preserved but Disabled After Agent Unpublish"
priority: critical
type: functional
module: agents-publishing
status: ready
execution_type: manual
tags: [feat:agents, story:3772, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3772]
---
# ELITEA-0199: TC-007: Existing Conversations Are Preserved but Disabled After Agent Unpublish

**Module:** Agents Publishing · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a user who had active conversations with a published agent can still view full conversation history after the agent is unpublished, but cannot send new messages — and an informational message is displayed.

Coverage:
- All prior message history visible and intact after unpublish
- Informational banner displayed: "This agent has been unpublished and is no longer available"
- Chat input field disabled — no new messages can be sent
- Send button absent or disabled
- No crash or 404 when navigating to an unpublished-agent conversation

## Preconditions

- User B has an existing conversation with the published version of Agent C (conversation has 3+ messages exchanged)
- User A (owner) unpublishes Agent C version 'v1.0'
- Logged in as User B

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | As User A, unpublish Agent C version 'v1.0' | Agent C unpublished successfully |
| 2 | Log in as User B | User B is logged in |
| 3 | Open User B's existing conversation with the now-unpublished Agent C | Conversation page loads without crash or 404 |
| 4 | Scroll through the conversation history | All prior messages (user and AI) are visible and content is intact |
| 5 | Look for an informational message/banner about the agent status | A message is displayed: 'This agent has been unpublished and is no longer available' (or equivalent wording) |
| 6 | Click on the message input field | Input field is disabled / read-only |
| 7 | Check for a Send button | Send button is absent or disabled — cannot be clicked |
| 8 | Attempt to type in the input field | No text can be entered |

## Expected Final State

No text can be entered

## Pass/Fail Criteria

PASS:
- Conversation page loads without error
- Full message history is visible and unchanged
- Informational "unpublished" message/banner is displayed
- Input field is disabled; no new messages can be sent

FAIL:
- Conversation page crashes, shows 404, or blank screen
- Prior message history is missing or corrupted
- No informational message about agent being unpublished
- User B can still send new messages despite agent being unpublished
