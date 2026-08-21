---
id: ELITEA-2365
title: "Agent Hub — My Liked reload button refreshes list with likes made in another tab"
priority: medium
type: functional
module: agent-hub
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:agent-hub]
requirements: []
automation_test_id:
  - tests.ui.agent_hub.test_agent_hub_my_liked_reload_cross_tab_sync.TestAgentHubMyLikedReloadCrossTabSync.test_agent_hub_my_liked_reload_reflects_cross_tab_like
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1232
---

# ELITEA-2365: Agent Hub — My Liked reload button refreshes list with likes made in another tab

**Module:** agent-hub · **Priority:** medium · **Type:** functional

**Objective:** Verify that Agent Hub — My Liked reload button refreshes list with likes made in another tab. Success is confirmed when verify the like count on the newly appeared agent card matches the count seen in tab b.

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
| 1 | Open Agent Hub in Browser Tab A and click the "My Liked" category filter tab | Target page/section loads successfully. |
| 2 | Verify the current list of liked agents is displayed under the "My Liked" section | Condition holds as described. |
| 3 | Open Agent Hub in Browser Tab B (new tab) | Target page/section loads successfully. |
| 4 | In Tab B, locate an agent that is not yet liked and click its heart icon to like it | Action completes without error and produces the expected UI state. |
| 5 | Verify the like count increments on the agent card in Tab B | Condition holds as described. |
| 6 | Switch back to Browser Tab A | Action completes without error and produces the expected UI state. |
| 7 | Verify the newly liked agent from Tab B is not yet visible in the "My Liked" list in Tab A | Condition holds as described. |
| 8 | Click the reload/refresh (↻) icon next to the "My Liked" section header in Tab A | Control responds; expected next state is shown. |
| 9 | Verify the "My Liked" list refreshes | Condition holds as described. |
| 10 | Verify the agent liked in Tab B now appears in the "My Liked" list in Tab A | Condition holds as described. |
| 11 | Verify the like count on the newly appeared agent card matches the count seen in Tab B | Condition holds as described. |

---

## Expected Final State

Verify the like count on the newly appeared agent card matches the count seen in Tab B.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Agent Hub — My Liked reload button refreshes list with likes made in another tab.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
