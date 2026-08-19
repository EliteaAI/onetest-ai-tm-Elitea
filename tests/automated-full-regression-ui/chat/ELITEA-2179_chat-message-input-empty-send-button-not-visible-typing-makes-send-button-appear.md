---
id: ELITEA-2179
title: "Chat – Message Input Field Empty – Send Button Not Visible and Typing Makes Send Button Appear"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id: "tests.ui.chat.test_streaming_response.TestStreamingResponse.test_composer_send_button_toggles_with_empty_input_and_waveform_reappears"
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1586
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2179: Chat – Message Input Field Empty – Send Button Not Visible and Typing Makes Send Button Appear

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify the Send button appears only when text is entered and disappears when the field is empty.

---

## Preconditions

- User is logged in to the Elitea platform.
- User has an open conversation.

---

## Test Data

| Field | Value |
|-------|-------|
| Test message | Hello |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Open a conversation and verify the message input field is empty | Input field empty |
| 2 | Verify the Send button (blue arrow) is NOT visible; waveform icon is on the far right | Send button hidden; waveform visible |
| 3 | Click inside the input field and type 'h' | Waveform replaced by blue Send button |
| 4 | Delete the character | Send button disappears; waveform reappears |
| 5 | Type 'Hello' and click Send | Message 'Hello' appears in conversation; input cleared; waveform reappears; LLM begins responding |

---

## Expected Final State

Send button appears on typing and disappears when field is cleared.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Send button behavior is correct.

**Fail:**
- Any step produces an error or unexpected result.
- Send button visible when field is empty or not visible when text is present.
