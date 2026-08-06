---
id: ELITEA-2363
title: "Agent Hub — search bar filters agents in real time"
priority: medium
type: functional
module: agent-hub
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:agent-hub]
requirements: []
automation_test_id:
  - tests.ui.agents.test_agent_hub_search_bar_filters_in_real_time.TestAgentHubSearchBarFiltersInRealTime.test_agent_hub_search_bar_filters_in_real_time
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1230
---

# ELITEA-2363: Agent Hub — search bar filters agents in real time

**Module:** agent-hub · **Priority:** medium · **Type:** functional

**Objective:** Verify that Agent Hub — search bar filters agents in real time. Success is confirmed when clear the search field and verify all agents return to the list.

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
| 2 | Click in the search bar at the top | Control responds; expected next state is shown. |
| 3 | Type a partial search term (e.g., "story") | Field accepts the input and displays the entered value. |
| 4 | Verify the agent list filters in real time as the user types | Condition holds as described. |
| 5 | Verify only matching agents are displayed (e.g., "User Story Creator") | Condition holds as described. |
| 6 | Clear the search field and verify all agents return to the list | Action completes without error and produces the expected UI state. |

---

## Expected Final State

Clear the search field and verify all agents return to the list.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Agent Hub — search bar filters agents in real time.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
