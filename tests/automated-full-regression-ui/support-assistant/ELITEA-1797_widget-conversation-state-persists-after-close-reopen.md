---
id: ELITEA-1797
title: "Widget conversation state persists after close and reopen"
priority: high
type: functional
module: support-assistant
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:support-assistant]
requirements: []
automation_test_id: tests.ui.support_assistant.test_support_assistant_smoke.TestSupportAssistantLauncher.test_widget_state_persists_after_close_reopen
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1651
---

# ELITEA-1797: Widget conversation state persists after close and reopen

**Module:** support-assistant · **Priority:** high · **Type:** functional

**Objective:** Verify that a conversation started in the Support Assistant widget is not lost when the user closes and then reopens the widget panel — the assistant's response messages are still present after the widget is reopened.

---

## Preconditions

- User is authenticated (browser context pre-loaded with `auth_state` via `page` fixture).
- Support Assistant feature is enabled.

---

## Test Data

| Field | Value |
|-------|-------|
| Test message | `"Test message for state persistence"` |
| Message input selector | `textbox[placeholder*="Type a message"]` |
| Assistant message count selector | `button[aria-label="Copy to clipboard"]` inside `.elitea-assistant-container` |
| Response wait timeout | 60 000 ms |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Chat page (`/chat`) | Page loads successfully |
| 2 | Open the Support Assistant widget | Widget panel opens; title is visible |
| 3 | Record the initial number of assistant messages | Baseline assistant message count is captured |
| 4 | Type and send the message `"Test message for state persistence"` | Message is submitted; Send button is clicked |
| 5 | Wait for the AI assistant to respond (up to 60 s) | At least one new "Copy to clipboard" button appears in the widget container |
| 6 | Assert that at least one new assistant message appeared | `get_assistant_message_count()` is greater than the initial count |
| 7 | Close the widget | Widget panel is dismissed; title is hidden |
| 8 | Reopen the widget by clicking the launcher | Widget panel reopens; title becomes visible |
| 9 | Wait for the widget to be fully ready (title + input visible, +2 s for messages to load) | Widget is ready; messages are rendered |
| 10 | Assert that the message count after reopening is at least as high as after sending | `get_assistant_message_count()` ≥ count recorded in step 5 |

---

## Expected Final State

The assistant response messages that were present before closing the widget are still visible when the widget is reopened. The conversation is not reset by toggling the widget open/closed.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Message count after reopen ≥ message count after sending.

**Fail:**
- Any step produces an error or unexpected result.
- Messages are lost after close/reopen (count drops below post-send count).
