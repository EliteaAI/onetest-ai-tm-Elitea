---
id: ELITEA-1798
title: "Send message and receive AI response via Send button"
priority: high
type: functional
module: support-assistant
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:support-assistant]
requirements: []
---

# ELITEA-1798: Send message and receive AI response via Send button

**Module:** support-assistant · **Priority:** high · **Type:** functional

**Objective:** Verify the end-to-end send-and-receive messaging flow: the user types a message, sends it via the Send button, the assistant generates a response (with the button disabled during generation), the response appears in the widget, and the input field is empty afterwards.

---

## Preconditions

- User is authenticated (browser context pre-loaded with `auth_state` via `page` fixture).
- Support Assistant feature is enabled.

---

## Test Data

| Field | Value |
|-------|-------|
| Test message | `"Hello, what is Elitea?"` |
| Message input selector | `textbox[placeholder*="Type a message"]` |
| Send button selector | `button[aria-label="Send message"]` |
| Response wait timeout | 60 000 ms |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Chat page (`/chat`) | Page loads successfully |
| 2 | Open the Support Assistant widget | Widget panel opens; title is visible |
| 3 | Wait for the widget to be fully ready | Title and `textbox[placeholder*="Type a message"]` are both visible |
| 4 | Record the initial number of assistant messages | Baseline assistant message count is captured |
| 5 | Type the message `"Hello, what is Elitea?"` in the input field | Text appears in the input field |
| 6 | Wait for the Send button to be enabled, then click it | `button[aria-label="Send message"]` is not disabled; click is performed |
| 7 | Wait for the AI assistant to deliver a complete response (up to 60 s) | A new "Copy to clipboard" button appears in the widget container; 1-second stabilisation wait completes |
| 8 | Assert that the assistant message count increased | `get_assistant_message_count()` is greater than the initial count |
| 9 | Assert that the message input field is empty | `is_input_empty()` returns `True`; input value length is 0 after stripping whitespace |

---

## Expected Final State

The user message is sent, the assistant returns a complete response (new "Copy to clipboard" button appears), and the message input field is cleared. The Send button becomes enabled again once the response is complete.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Assistant message count increases after send.
- Input field is empty after the response is received.

**Fail:**
- Any step produces an error or unexpected result.
- No assistant response appears within the timeout.
- Input field is not cleared after sending.
