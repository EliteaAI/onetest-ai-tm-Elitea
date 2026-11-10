---
id: ELITEA-2356
title: "Catalog — open agent detail modal"
priority: medium
type: functional
module: agent-hub
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:agent-hub]
requirements: []
automation_test_id:
  - tests.ui.agent_hub.test_agent_hub_open_agent_detail_modal.TestAgentHubOpenAgentDetailModal.test_agent_hub_open_agent_detail_modal
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1220
---

# ELITEA-2356: Catalog — open agent detail modal

**Module:** agent-hub · **Priority:** medium · **Type:** functional

**Objective:** Verify that Catalog — open agent detail modal. Success is confirmed when verify the "start conversation" button is visible at the bottom of the modal.

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
| 1 | Navigate to Catalog (the Agents tab is active) | Catalog loads on the Agents tab (selected). |
| 2 | Click on any agent card (e.g., "User Story Creator") | Control responds; expected next state is shown. |
| 3 | Verify the agent detail modal opens as an overlay | Condition holds as described. |
| 4 | Verify the modal displays agent icon, agent name, owner name, liked status, copy link icon, "x" cutton and description | Condition holds as described. |
| 5 | Verify the modal shows a "CONVERSATION STARTERS" section | Condition holds as described. |
| 6 | Verify the modal shows a "WELCOME MESSAGE" section | Condition holds as described. |
| 7 | Verify the "Start conversation" button is visible at the bottom of the modal | Condition holds as described. |

---

## Expected Final State

Verify the "Start conversation" button is visible at the bottom of the modal.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Catalog — open agent detail modal.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
