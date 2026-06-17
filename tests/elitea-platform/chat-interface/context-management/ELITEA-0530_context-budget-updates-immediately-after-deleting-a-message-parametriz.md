---
id: ELITEA-0530
title: "Context Budget Updates Immediately After Deleting a Message [Parametrized: Chat / Agent / Pipeline]"
priority: high
type: functional
module: context-management
status: ready
execution_type: manual
tags: [feat:pipelines, eng:frontend, feat:agents, feat:chat]
requirements: [ProjectAlita/projectalita.github.io#3938]
---
# ELITEA-0530: Context Budget Updates Immediately After Deleting a Message [Parametrized: Chat / Agent / Pipeline]

**Module:** Context Management · **Priority:** High · **Type:** Functional

**Objective:** Verify that after deleting a message from a conversation, the context budget immediately reflects the updated token count and message data — without requiring a new message to be sent — across Direct Chat, Agent Chat, and Pipeline Chat pages.

**Coverage:**
- Context budget updates immediately after message deletion (no next-request trigger required)
- Token count and message data reflect the deletion in real time
- Behavior verified across Direct Chat, Agent Chat, and Pipeline Chat pages

## Preconditions

- User is logged in to ELITEA (Dev or Stage environment)
- A conversation with at least 3 user/assistant message exchanges exists and is open
- Context budget panel is expanded and visible, showing non-zero values
- Run for each context: Direct Chat page, Agent Chat page, Pipeline Chat page
- Browser: Chrome (latest stable)

## Test Data

| Item | Value |
|---|---|
| Environment | Dev: {{base_url}} / Stage: {{base_url}} |
| Conversation | Any chat/agent/pipeline with at least 3 message exchanges |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a conversation with at least 3 message exchanges. Expand the context budget panel. | Context budget is visible and shows non-zero values (message count, token usage). |
| 2 | Note the current context budget values: message count and total token usage. | Values are recorded for comparison. |
| 3 | Delete one message from the conversation (e.g., delete the most recent user/assistant exchange). | The message is removed from the conversation UI. |
| 4 | Immediately observe the context budget panel — do not send a new message. | Context budget immediately reflects the deletion — message count decreases and token usage updates to match the new conversation state. |
| 5 | Confirm the updated values are different from those noted in Step 2 and accurately reflect the remaining conversation. | Context budget values match the post-deletion conversation (fewer messages, lower token count). |
| 6 | Repeat Steps 1–5 on the Agent Chat page. | Same immediate context budget update behavior after deletion. |
| 7 | Repeat Steps 1–5 on the Pipeline Chat page. | Same immediate context budget update behavior after deletion. |

## Expected Final State

Same immediate context budget update behavior after deletion.

## Pass/Fail Criteria

**Pass:**
- Context budget updates immediately after message deletion on all three pages (Chat, Agent, Pipeline)
- No new message needs to be sent to trigger the update
- Updated values correctly reflect the reduced message count and token usage

**Fail:**
- Context budget only updates after a new message is sent on any of the three pages
- Token count or message count remains unchanged after deletion
- Any page shows a different/inconsistent update behavior compared to the others
