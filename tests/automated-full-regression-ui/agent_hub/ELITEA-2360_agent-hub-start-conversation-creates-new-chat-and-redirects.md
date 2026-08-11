---
id: ELITEA-2360
title: "Agent Hub — start conversation creates new chat and redirects to Chat page"
priority: medium
type: functional
module: agent-hub
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:agent-hub]
requirements: []
automation_test_id:
  - tests.ui.agent_hub.test_agent_hub_start_conversation_creates_new_chat.TestAgentHubStartConversationCreatesNewChat.test_agent_hub_start_conversation_creates_new_chat
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1433
---

# ELITEA-2360: Agent Hub — start conversation creates new chat and redirects to Chat page

**Module:** agent-hub · **Priority:** medium · **Type:** functional

**Objective:** Verify that Agent Hub — start conversation creates new chat and redirects to Chat page. Success is confirmed when verify the chat welcome message is displayed (e.g., "hello, [username]! what can i do for you today?").

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
| 1 | Navigate to Agent Hub | Target page/section loads successfully. |
| 2 | Click on an agent card (e.g., "User Story Creator") to open the detail modal | Control responds; expected next state is shown. |
| 3 | Click the "Start conversation" button | Control responds; expected next state is shown. |
| 4 | Verify a new chat conversation is created | Condition holds as described. |
| 5 | Verify the user is redirected to the Chat interface | Condition holds as described. |
| 6 | Verify the chat welcome message is displayed (e.g., "Hello, [username]! What can I do for you today?") | Condition holds as described. |

---

## Expected Final State

Verify the chat welcome message is displayed (e.g., "Hello, [username]! What can I do for you today?").

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Agent Hub — start conversation creates new chat and redirects to Chat page.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
