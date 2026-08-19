---
id: ELITEA-2469
title: "Chat – Select agent from # list adds it to participants and it can respond"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id:
  - "tests.ui.chat.test_chat_interface.TestHashSearch.test_add_agent_via_hash_search_joins_participants_and_responds"
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1601
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2469: Chat – Select agent from # list adds it to participants and it can respond

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that Chat – Select agent from # list adds it to participants and it can respond. Success is confirmed when verify the agent responds and remains in the participants panel.

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
| 1 | Navigate to the Chats section and create a new conversation | Target page/section loads successfully. |
| 2 | Verify the PARTICIPANTS panel shows no AGENTS section initially | Condition holds as described. |
| 3 | Type "#" in the message input field and click on an agent from the "SEARCH RESULTS" dropdown | Field accepts the input and displays the entered value. |
| 4 | Verify the agent name appears in the message input field with # mention | Condition holds as described. |
| 5 | Verify the PARTICIPANTS panel now shows an AGENTS section with the selected agent listed with name, version, and icon | Condition holds as described. |
| 6 | Type a message (e.g. "hello") and send it | Field accepts the input and displays the entered value. |
| 7 | Verify the agent responds and remains in the PARTICIPANTS panel | Condition holds as described. |

---

## Expected Final State

Verify the agent responds and remains in the PARTICIPANTS panel.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Chat – Select agent from # list adds it to participants and it can respond.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
