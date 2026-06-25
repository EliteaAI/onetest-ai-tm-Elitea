---
id: ELITEA-0643
title: "Conversation is retained when the Support Assistant panel is closed and reopened"
priority: high
type: functional
module: elitea-chat-bot
status: ready
execution_type: automated
automation_test_id:
  - test_support_assistant_smoke.py:TestSupportAssistantSmoke.test_widget_state_persists_after_close_reopen
  - test_support_assistant_smoke.py:TestSupportAssistantSmoke.test_history_restore_and_continue
tags: [session-continuity, state-persistence, open-close, R-2.0.3]
requirements: [EliteaAI/elitea_issues#4775, EliteaAI/elitea_issues#4774]
---
# ELITEA-0643: Conversation is retained when the Support Assistant panel is closed and reopened

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Closing the Support Assistant panel by clicking the X button and then reopening it must restore the full conversation exactly as it was. If messages are lost on close, users cannot safely close the panel without fear of losing their support thread.

## Preconditions

- Logged in to ELITEA ({{base_url}}
- Support Assistant panel is open with at least one completed message exchange (user message + assistant response visible)

## Test Data

- Any existing conversation with at least 2 messages

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Confirm the current conversation has at least one user message and one assistant response visible in the panel. Note the text of those messages. | Messages visible and noted. |
| 2 | Click the X (Close) button at the top of the Support Assistant panel. | The panel closes. The launcher icon is visible at the bottom of the sidebar. |
| 3 | Click the launcher icon to reopen the Support Assistant panel. | The panel opens. |
| 4 | Observe the message area. | The exact same messages noted in step 1 are present. Nothing is missing. No new welcome message has replaced the conversation. |
| 5 | Send a follow-up message and wait for the response. | The follow-up is added to the existing conversation. The assistant responds with awareness of the prior messages (context retained). |

## Expected Final State

The follow-up is added to the existing conversation. The assistant responds with awareness of the prior messages (context retained).

## Pass/Fail Criteria

Pass:
- All messages from before closing are present after reopening
- The assistant's response to the follow-up references prior context, confirming the session was not reset

Fail:
- Conversation is empty after reopening (messages lost)
- Welcome message replaces the prior conversation on reopen
- The follow-up message is treated as the first message (no prior context)
