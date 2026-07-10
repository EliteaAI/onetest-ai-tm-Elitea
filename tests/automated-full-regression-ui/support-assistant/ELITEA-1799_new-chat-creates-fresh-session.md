---
id: ELITEA-1799
title: "New Chat button creates fresh session and moves previous to history"
priority: high
type: functional
module: support-assistant
status: draft
execution_type: automated
automation_test_id: tests.ui.support_assistant.test_support_assistant_smoke.TestSupportAssistantNewSession.test_new_chat_creates_fresh_session
tags: [automated:UI:regression, feat:support-assistant]
requirements: []
---

# ELITEA-1799: New Chat button creates fresh session and moves previous to history

**Module:** support-assistant · **Priority:** high · **Type:** functional

**Objective:** Verify that clicking the New Chat button, after an active conversation has at least one assistant reply, moves the current conversation to history and presents the user with a clean slate (empty or welcome state) for a new support session.

---

## Preconditions

- User is authenticated (browser context pre-loaded with `auth_state` via `page` fixture).
- Support Assistant feature is enabled.

---

## Test Data

| Field | Value |
|-------|-------|
| Test message | `"Test message before new chat"` |
| New Chat button selector | `button[data-testid="support-assistant-new-chat"]` |
| Response wait timeout | 60 000 ms |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Chat page (`/chat`) | Page loads successfully |
| 2 | Open the Support Assistant widget | Widget panel opens; title is visible |
| 3 | Wait for the widget to be fully ready | Widget title and message input are visible |
| 4 | Record the initial number of assistant messages | Baseline assistant message count is captured |
| 5 | Send the message `"Test message before new chat"` | Message is submitted via Send button |
| 6 | Wait for the AI response (up to 60 s) | At least one new assistant message appears |
| 7 | Assert that at least one new assistant message appeared | `get_assistant_message_count()` exceeds the initial count |
| 8 | Click the New Chat button (`data-testid="support-assistant-new-chat"` or `aria-label="New chat"`) | New Chat action is triggered; 1-second wait then network idle is reached |
| 9 | Wait 1 s for session reset, then wait for the widget to be ready again | Widget re-enters a ready state with an empty or welcome conversation |

---

## Expected Final State

After clicking New Chat, the old conversation messages are no longer displayed in the main chat area. The widget enters a fresh state (empty conversation or welcome message). The previous session is preserved in history and not lost.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Old messages are cleared from the active view after New Chat.
- Widget is in a clean/ready state for a new conversation.

**Fail:**
- Any step produces an error or unexpected result.
- Old messages remain visible after clicking New Chat.
- Widget is not in a usable state after the session reset.
