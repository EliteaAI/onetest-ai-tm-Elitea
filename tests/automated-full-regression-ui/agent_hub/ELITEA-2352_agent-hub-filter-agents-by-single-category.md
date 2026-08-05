---
id: ELITEA-2352
title: "Agent Hub — filter agents by single category"
priority: medium
type: functional
module: agent-hub
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:agent-hub]
requirements: []
automation_test_id:
  - tests.ui.agents.test_agent_hub_filter_single_category.TestAgentHubFilterSingleCategory.test_agent_hub_filter_by_single_category
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1214
---

# ELITEA-2352: Agent Hub — filter agents by single category

**Module:** agent-hub · **Priority:** medium · **Type:** functional

**Objective:** Verify that Agent Hub — filter agents by single category. Success is confirmed when verify the section header "business analyst" appears above the results with "reload category items" icon next to it.

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
| 2 | Click on "Business Analyst" category filter tab | Control responds; expected next state is shown. |
| 3 | Verify the selected tab is highlighted/active | Condition holds as described. |
| 4 | Verify only Business Analyst agents are displayed (e.g., AI Platform Design Advisor, User Story Creator, Business Analyst) | Condition holds as described. |
| 5 | Verify the section header "Business Analyst" appears above the results with "reload category items" icon next to it | Condition holds as described. |

---

## Expected Final State

Verify the section header "Business Analyst" appears above the results with "reload category items" icon next to it.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Agent Hub — filter agents by single category.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
