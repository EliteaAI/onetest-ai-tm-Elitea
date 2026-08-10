---
id: ELITEA-2358
title: "Agent Hub — like an agent from the expanded detail modal"
priority: medium
type: functional
module: agent-hub
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:agent-hub]
requirements: []
automation_test_id:
  - tests.ui.agents.test_agent_hub_like_agent_from_modal.TestAgentHubLikeAgentFromModal.test_agent_hub_like_agent_from_modal
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1415
---

# ELITEA-2358: Agent Hub — like an agent from the expanded detail modal

**Module:** agent-hub · **Priority:** medium · **Type:** functional

**Objective:** Verify that Agent Hub — like an agent from the expanded detail modal. Success is confirmed when close the modal and verify the updated like count is reflected on the agent card in the list.

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
| 2 | Click on any agent card to open the detail modal | Control responds; expected next state is shown. |
| 3 | Locate the heart icon in the modal header showing the current like count | Action completes without error and produces the expected UI state. |
| 4 | Click the heart icon | Control responds; expected next state is shown. |
| 5 | Verify the like count increments by 1 in the modal header | Condition holds as described. |
| 6 | Close the modal and verify the updated like count is reflected on the agent card in the list | Action completes without error and produces the expected UI state. |

---

## Expected Final State

Close the modal and verify the updated like count is reflected on the agent card in the list.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Agent Hub — like an agent from the expanded detail modal.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
