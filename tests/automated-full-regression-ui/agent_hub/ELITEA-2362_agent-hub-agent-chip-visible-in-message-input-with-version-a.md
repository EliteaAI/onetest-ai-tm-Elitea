---
id: ELITEA-2362
title: "Agent Hub — agent chip visible in message input with version and settings"
priority: medium
type: functional
module: agent-hub
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:agent-hub]
requirements: []
automation_test_id:
  - tests.ui.agent_hub.test_agent_hub_agent_chip_visible_in_message_input.TestAgentHubAgentChipVisibleInMessageInput.test_agent_chip_visible_in_message_input
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1436
---

# ELITEA-2362: Agent Hub — agent chip visible in message input with version and settings

**Module:** agent-hub · **Priority:** medium · **Type:** functional

**Objective:** Verify that Agent Hub — agent chip visible in message input with version and settings. Success is confirmed when verify a settings icon is visible on the agent chip.

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
| 3 | Click "Start conversation" | Control responds; expected next state is shown. |
| 4 | Verify the agent chip is visible in the message input area at the bottom | Condition holds as described. |
| 5 | Verify the chip displays the agent avatar/icon | Condition holds as described. |
| 6 | Verify the chip displays the agent name (e.g., "User Story Creator") | Condition holds as described. |
| 7 | Verify the chip displays the agent version (e.g., "ver-0.1") | Condition holds as described. |
| 8 | Verify a settings icon is visible on the agent chip | Condition holds as described. |

---

## Expected Final State

Verify a settings icon is visible on the agent chip.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Agent Hub — agent chip visible in message input with version and settings.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
