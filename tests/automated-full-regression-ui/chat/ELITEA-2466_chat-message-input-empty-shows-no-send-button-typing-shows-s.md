---
id: ELITEA-2466
title: "Chat – Message input empty shows no send button; typing shows send button; send clears field"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2466: Chat – Message input empty shows no send button; typing shows send button; send clears field

**Module:** chat-interface · **Priority:** critical · **Type:** functional

**Objective:** Verify that Chat – Message input empty shows no send button; typing shows send button; send clears field. Success is confirmed when verify the waveform/audio icon reappears and a response begins generating from the llm.

---

## Preconditions

- User is logged in to the Elitea platform.


---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Chats section and open any existing conversation | Target page/section loads successfully. |
| 2 | Verify the message input field is empty and the Send button is NOT visible | Condition holds as described. |
| 3 | Verify the bottom bar shows: + icon on the left, current LLM name with model icon, gear icon, microphone icon, and a waveform/audio icon on the far right | Condition holds as described. |
| 4 | Click inside the message input field and verify it becomes focused with a teal/cyan border | Control responds; expected next state is shown. |
| 5 | Type any character (e.g. "h") and verify the waveform/audio icon is replaced by the blue Send button | Field accepts the input and displays the entered value. |
| 6 | Delete the typed character and verify the Send button disappears and the waveform/audio icon reappears | Operation completes successfully; state updates and confirmation is shown. |
| 7 | Type a message (e.g. "Hello") and click the Send button | Field accepts the input and displays the entered value. |
| 8 | Verify the message appears in the conversation history with the sender's name and avatar | Condition holds as described. |
| 9 | Verify the message input field is cleared after sending and the Send button disappears | Condition holds as described. |
| 10 | Verify the waveform/audio icon reappears and a response begins generating from the LLM | Condition holds as described. |

---

## Expected Final State

Verify the waveform/audio icon reappears and a response begins generating from the LLM.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Chat – Message input empty shows no send button; typing shows send button; send clears field.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
