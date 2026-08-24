---
id: ELITEA-2681
title: "Stop button correctly handles messages stopped at different AI response phases"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.6, issue:5000]
requirements: [EliteaAI/elitea_issues#5000]
---
# ELITEA-2681: Stop button correctly handles messages stopped at different AI response phases

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that Stop button correctly restores messages when clicked at different points during AI response generation — immediately after sending, during early response, mid-response, and near completion.

## Preconditions

- User is logged in to `{{base_url}}`
- Regular chat interface is accessible

## Test Data

Test clicking Stop at different timing:

| Timing Phase | Wait Duration After Send | Description |
|--------------|--------------------------|-------------|
| Immediate | 0-1 seconds | Click Stop right after clicking Send |
| Early response | 2-3 seconds | Click Stop after AI starts responding |
| Mid response | 5-10 seconds | Click Stop during active AI response streaming |
| Near completion | Wait until response is ~80-90% complete | Click Stop when response is almost complete |

## Steps

For **each timing phase** in the Test Data table:

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open regular chat interface (or refresh to reset state) | Chat interface loads successfully |
| 2 | Type "Test message for timing" in the input field | Text appears in the input field |
| 3 | Click Send button | Message is sent; AI response processing begins |
| 4 | Wait for the duration specified in the current timing phase | Time elapses as specified (0-1s, 2-3s, 5-10s, or ~90% response) |
| 5 | Click Stop button at the designated timing | Stop button is clicked successfully |
| 6 | Verify the user message is removed from the chat thread | User message "Test message for timing" is not visible in the thread |
| 7 | Verify the message is restored to the input field | "Test message for timing" appears in the input field |
| 8 | Verify any partial AI response is removed from the thread | No partial AI text remains visible in the chat thread |
| 9 | Verify no UI errors or glitches occur | No error messages, UI freezing, or visual artifacts |
| 10 | Click in the input field and verify it is editable | Cursor appears; text can be edited |

## Expected Final State

Across all timing phases, the behavior is consistent: user message is removed from thread, restored to input field, partial AI response is cleared, and the UI remains stable.

## Pass/Fail Criteria

**Pass:**
- Stop works correctly at all four timing phases
- User message is restored to input field in every case
- Partial AI responses are removed regardless of response length
- No UI errors, glitches, or freezing
- Input field is editable after each stop

**Fail:**
- Stop fails at any timing phase
- Message is not restored at any phase
- Partial AI response remains visible
- UI errors, freezing, or visual glitches occur
- Input field is not editable after stopping
