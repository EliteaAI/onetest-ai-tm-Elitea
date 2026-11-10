---
id: ELITEA-2354
title: "Catalog — like an agent from the list view"
priority: medium
type: functional
module: agent-hub
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:agent-hub]
requirements: []
automation_test_id:
  - tests.ui.agent_hub.test_agent_hub_like_agent_list_view.TestAgentHubLikeAgentListView.test_agent_hub_like_agent_from_list_view
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1216
---

# ELITEA-2354: Catalog — like an agent from the list view

**Module:** agent-hub · **Priority:** medium · **Type:** functional

**Objective:** Verify that Catalog — like an agent from the list view. Success is confirmed when refresh the page and verify the updated like count persists.

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
| 2 | Locate an agent card showing 0 likes (e.g., "AI Platform Design Advisor") | Action completes without error and produces the expected UI state. |
| 3 | Click the heart icon on the agent card | Control responds; expected next state is shown. |
| 4 | Verify the heart icon changes to a filled/active state | Condition holds as described. |
| 5 | Verify the like count increments by 1 | Condition holds as described. |
| 6 | Refresh the page and verify the updated like count persists | Action completes without error and produces the expected UI state. |

---

## Expected Final State

Refresh the page and verify the updated like count persists.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Catalog — like an agent from the list view.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
