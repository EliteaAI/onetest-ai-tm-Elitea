---
id: ELITEA-2350
title: "Agent Hub — page loads successfully for Private project"
priority: high
type: functional
module: agent-hub
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:agent-hub]
requirements: []
automation_test_id:
  - tests.ui.agent_hub.test_agent_hub_page_loads_private_project.TestAgentHubPageLoadsPrivateProject.test_agent_hub_page_loads_private_project
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1211
---

# ELITEA-2350: Agent Hub — page loads successfully for Private project

**Module:** agent-hub · **Priority:** high · **Type:** functional

**Objective:** Verify that Agent Hub — page loads successfully for Private project. Success is confirmed when verify agent cards are displayed in the main content area.

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
| 1 | Navigate to Agent Hub from a Private project context | Target page/section loads successfully. |
| 2 | Verify the page loads with "Welcome to Agent HUB" header | Condition holds as described. |
| 3 | Verify the search bar is visible at the top center | Condition holds as described. |
| 4 | Verify category filter tabs are displayed: Trending, My Liked, Business Analyst, DevOps, Development, Elitea, Epam, Knowledge & Documentation, Project Management, Quality Assurance, Other | Condition holds as described. |
| 5 | Verify agent cards are displayed in the main content area | Condition holds as described. |

---

## Expected Final State

Verify agent cards are displayed in the main content area.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Agent Hub — page loads successfully for Private project.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
