---
id: ELITEA-2364
title: "Agent Hub — My Liked filter shows only liked agents"
priority: medium
type: functional
module: agent-hub
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:agent-hub]
requirements: []
automation_test_id:
  - tests.ui.agent_hub.test_agent_hub_my_liked_filter_shows_only_liked_agents.TestAgentHubMyLikedFilterShowsOnlyLikedAgents.test_agent_hub_my_liked_filter_shows_only_liked_agents
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1415
---

# ELITEA-2364: Agent Hub — My Liked filter shows only liked agents

**Module:** agent-hub · **Priority:** medium · **Type:** functional

**Objective:** Verify that Agent Hub — My Liked filter shows only liked agents. Success is confirmed when unlike an agent while in the my liked view and verify it is removed from the list.

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
| 2 | Like at least one agent from the list | Action completes without error and produces the expected UI state. |
| 3 | Click the "My Liked" category filter tab | Control responds; expected next state is shown. |
| 4 | Verify only agents liked by the current user are displayed | Condition holds as described. |
| 5 | Unlike an agent while in the My Liked view and verify it is removed from the list | Action completes without error and produces the expected UI state. |

---

## Expected Final State

Unlike an agent while in the My Liked view and verify it is removed from the list.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Agent Hub — My Liked filter shows only liked agents.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
