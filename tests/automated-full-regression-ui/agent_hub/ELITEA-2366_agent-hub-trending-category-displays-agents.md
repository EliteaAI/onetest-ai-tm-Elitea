---
id: ELITEA-2366
title: "Agent Hub — Trending category displays agents"
priority: medium
type: functional
module: agent-hub
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:agent-hub]
requirements: []
automation_test_id:
  - tests.ui.agent-hub.test_agent_hub_trending_category.TestAgentHubTrendingCategory.test_agent_hub_trending_category_displays_agents
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1429
---

# ELITEA-2366: Agent Hub — Trending category displays agents

**Module:** agent-hub · **Priority:** medium · **Type:** functional

**Objective:** Verify that Agent Hub — Trending category displays agents. Success is confirmed when verify the section header "trending" appears above the results with "reload the category items" next to it.

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
| 2 | Click the "Trending" category filter tab | Control responds; expected next state is shown. |
| 3 | Verify the tab is highlighted/active | Condition holds as described. |
| 4 | Verify agents are displayed under the Trending section | Condition holds as described. |
| 5 | Verify the section header "Trending" appears above the results with "Reload the category items" next to it | Condition holds as described. |

---

## Expected Final State

Verify the section header "Trending" appears above the results with "Reload the category items" next to it.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Agent Hub — Trending category displays agents.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
