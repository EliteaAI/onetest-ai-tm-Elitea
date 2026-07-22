---
id: ELITEA-2470
title: "Chat – Select pipeline from # list adds it to participants and it can respond"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2470: Chat – Select pipeline from # list adds it to participants and it can respond

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that Chat – Select pipeline from # list adds it to participants and it can respond. Success is confirmed when verify the pipeline processes and responds and remains in the participants panel.

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
| 1 | Navigate to the Chats section and create or open a conversation | Target page/section loads successfully. |
| 2 | Verify the PARTICIPANTS panel shows no PIPELINES section initially | Condition holds as described. |
| 3 | Type "#" in the message input field and click on a pipeline from the "SEARCH RESULTS" dropdown | Field accepts the input and displays the entered value. |
| 4 | Verify the pipeline name appears in the message input field with # mention | Condition holds as described. |
| 5 | Verify the PARTICIPANTS panel now shows a PIPELINES section with the selected pipeline listed with name and icon | Condition holds as described. |
| 6 | Type a message and send it | Field accepts the input and displays the entered value. |
| 7 | Verify the pipeline processes and responds and remains in the PARTICIPANTS panel | Condition holds as described. |

---

## Expected Final State

Verify the pipeline processes and responds and remains in the PARTICIPANTS panel.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Chat – Select pipeline from # list adds it to participants and it can respond.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
