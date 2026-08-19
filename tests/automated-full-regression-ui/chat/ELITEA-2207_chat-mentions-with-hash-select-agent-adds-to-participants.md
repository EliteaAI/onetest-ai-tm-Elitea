---
id: ELITEA-2207
title: "Chat – Mentions with # – Select Agent from List and Verify Agent is Added to Participants"
priority: medium
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

# ELITEA-2207: Chat – Mentions with # – Select Agent from List and Verify Agent is Added to Participants

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that selecting an agent from the '#' dropdown adds it to the PARTICIPANTS panel.

---

## Preconditions

- User is logged in to the Elitea platform.
- Agents exist in the project.

---

## Test Data

| Field | Value |
|-------|-------|
| Test message | hello |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Create a new conversation; verify no AGENTS in PARTICIPANTS | No AGENTS section |
| 2 | Type '#' and click an agent from the dropdown | Agent name appears in message field with # mention; AGENTS section added to PARTICIPANTS |
| 3 | Type 'hello' and send the message | Agent responds; remains in PARTICIPANTS |

---

## Expected Final State

Agent added to PARTICIPANTS via '#' mention.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Agent added to PARTICIPANTS; responds to message.

**Fail:**
- Any step produces an error or unexpected result.
- Agent not added or not responding.
