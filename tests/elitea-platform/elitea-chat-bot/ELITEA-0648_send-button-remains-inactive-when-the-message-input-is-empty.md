---
id: ELITEA-0648
title: "Send button remains inactive when the message input is empty"
priority: high
type: functional
module: elitea-chat-bot
status: ready
execution_type: manual
tags: [input-validation, empty-message, composer, R-2.0.3]
requirements: [#4775]
---
# ELITEA-0648: Send button remains inactive when the message input is empty

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** The Send button must stay inactive until the user has typed something in the input field. Sending an empty message serves no purpose and would trigger a needless API call. This also verifies the basic input guard of the composer.

## Preconditions

- Logged in to ELITEA ({{base_url}}
- Support Assistant panel is open

## Test Data

N/A (the test specifically uses an empty input)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Support Assistant panel and observe the message input field and Send button before typing anything. | The input field is empty showing placeholder text. The Send button appears greyed out or visually disabled. |
| 2 | Click the Send button while the input is empty. | Nothing happens. No message is submitted. No loading indicator appears. |
| 3 | Press the Enter key while the input field is empty and has focus. | No message is submitted. The conversation remains unchanged. |
| 4 | Type the letter "A" into the message input field. | The Send button becomes active/highlighted, indicating it can now be clicked. |
| 5 | Delete the character so the input field is empty again. | The Send button returns to its inactive/greyed-out state. |

## Expected Final State

The Send button returns to its inactive/greyed-out state.

## Pass/Fail Criteria

Pass:
- Send button is visually inactive with an empty input
- Clicking Send or pressing Enter with an empty input does nothing
- Send button activates as soon as any character is entered
- Send button deactivates again when input is cleared

Fail:
- Send button is active with an empty input
- An empty message appears in the conversation
- An API call is triggered on empty submit
