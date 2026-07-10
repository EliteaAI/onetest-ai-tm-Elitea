---
id: ELITEA-1800
title: "History restore — open previous session and continue messaging"
priority: high
type: functional
module: support-assistant
status: draft
execution_type: automated
automation_test_id: tests.ui.support_assistant.test_support_assistant_smoke.TestSupportAssistantHistory.test_history_restore_and_continue_messaging
tags: [automated:UI:regression, feat:support-assistant]
requirements: []
---

# ELITEA-1800: History restore — open previous session and continue messaging

**Module:** support-assistant · **Priority:** high · **Type:** functional

**Objective:** Verify the full history workflow: a conversation is created, moved to history via New Chat, the history panel is opened, the previous session is selected and its messages are restored, and the user can continue chatting within the restored session.

---

## Preconditions

- User is authenticated (browser context pre-loaded with `auth_state` via `page` fixture).
- Support Assistant feature is enabled.

---

## Test Data

| Field | Value |
|-------|-------|
| Initial message | `"History test message - distinctive content 12345"` |
| Follow-up message | `"Follow-up message after restore"` |
| History button selector | `button[data-testid="support-assistant-history"]` |
| New Chat button selector | `button[data-testid="support-assistant-new-chat"]` |
| Response wait timeout | 60 000 ms |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Chat page (`/chat`) | Page loads successfully |
| 2 | Open the Support Assistant widget | Widget panel opens; title is visible |
| 3 | Wait for widget ready | Widget title and message input are visible |
| 4 | Record the initial number of assistant messages | Baseline count is captured |
| 5 | Send the message `"History test message - distinctive content 12345"` | Message is submitted |
| 6 | Wait for the AI response (up to 60 s) | At least one new assistant message appears |
| 7 | Click the New Chat button to push the session into history | Current session moves to history; new session starts |
| 8 | Wait 1 s for session transition | Transition completes |
| 9 | Click the History button (`data-testid="support-assistant-history"` or `aria-label="Chat history"`) | History panel opens; 0.5 s transition wait completes |
| 10 | Assert that at least one history session is present | `get_history_session_count()` ≥ 1 |
| 11 | Select the most recent session (index 0) from the history list | First history item is clicked; network idle is reached |
| 12 | Assert that the restored session contains assistant messages | `get_assistant_message_count()` > 0 |
| 13 | Send the follow-up message `"Follow-up message after restore"` | Message is submitted in the restored session |
| 14 | Wait for the new AI response (up to 60 s) | At least one new assistant message appears beyond the restored count |
| 15 | Assert that the new reply was added to the restored session | `get_assistant_message_count()` exceeds the count recorded after step 12 |

---

## Expected Final State

The history panel shows at least one past session. Opening the most recent session displays the assistant messages from that session. A follow-up message sent in the restored session receives an AI response, confirming the restored session is fully interactive.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- History panel shows ≥ 1 session after New Chat.
- Restored session contains messages.
- Follow-up message in restored session receives a response.

**Fail:**
- Any step produces an error or unexpected result.
- No sessions appear in the history panel.
- Restored session is empty or the follow-up message does not receive a response.
