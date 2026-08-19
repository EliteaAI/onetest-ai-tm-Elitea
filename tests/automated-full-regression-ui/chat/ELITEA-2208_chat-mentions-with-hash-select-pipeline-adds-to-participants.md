---
id: ELITEA-2208
title: "Chat – Mentions with # – Select Pipeline from List and Verify Pipeline is Added to Participants"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id:
  - "tests.ui.chat.test_chat_interface.TestHashSearch.test_add_pipeline_via_hash_search_joins_participants_and_responds"
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1601
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2208: Chat – Mentions with # – Select Pipeline from List and Verify Pipeline is Added to Participants

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that selecting a pipeline from the '#' dropdown adds it to the PARTICIPANTS panel.

---

## Preconditions

- User is logged in to the Elitea platform.
- Pipelines exist in the project.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Create or open a conversation; verify no PIPELINES in PARTICIPANTS | No PIPELINES section |
| 2 | Type '#' and click a pipeline from the dropdown | Pipeline name in message field; PIPELINES section added to PARTICIPANTS |
| 3 | Type a message and send | Pipeline processes and responds; remains in PARTICIPANTS |

---

## Expected Final State

Pipeline added to PARTICIPANTS via '#' mention.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Pipeline added to PARTICIPANTS via '#'.

**Fail:**
- Any step produces an error or unexpected result.
- Pipeline not added or not responding.
