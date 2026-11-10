---
id: ELITEA-2357
title: "Catalog — close agent detail modal with X button"
priority: high
type: functional
module: agent-hub
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:agent-hub]
requirements: []
automation_test_id:
  - tests.ui.agent_hub.test_agent_hub_close_agent_detail_modal.TestAgentHubCloseAgentDetailModal.test_agent_hub_close_agent_detail_modal
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1415
---

# ELITEA-2357: Catalog — close agent detail modal with X button

**Module:** agent-hub · **Priority:** high · **Type:** functional

**Objective:** Verify that Catalog — close agent detail modal with X button. Success is confirmed when verify the user remains on the Catalog list view.

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
| 2 | Click on any agent card to open the detail modal | Control responds; expected next state is shown. |
| 3 | Verify the modal is displayed | Condition holds as described. |
| 4 | Click the X button in the top-right corner of the modal | Control responds; expected next state is shown. |
| 5 | Verify the modal closes | Condition holds as described. |
| 6 | Verify the user remains on the Catalog list view | Condition holds as described. |

---

## Expected Final State

Verify the user remains on the Catalog list view.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Catalog — close agent detail modal with X button.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
