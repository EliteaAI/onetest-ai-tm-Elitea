---
id: ELITEA-1884
title: "Remove a variable and verify removal persists"
priority: low
type: functional
module: agents
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:agents]
requirements: []
automation_test_id: tests.ui.agents.test_agent_remove_variable.TestAgentRemoveVariable.test_remove_variable_and_verify_removal_persists
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/536
---

# ELITEA-1884: Remove a variable and verify removal persists

**Module:** agents · **Priority:** low · **Type:** functional

**Objective:** Verify that removing a variable reference from the Instructions field causes the variable row to disappear, and that this removal persists after saving and reloading.

---

## Preconditions

- User is logged in to the Elitea platform.
- An agent with at least one saved variable exists.

---

## Test Data

| Field | Value |
|-------|-------|
| Variable to remove | {{variable}} (any existing variable reference) |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to an agent with at least one saved variable | The agent detail page loads with the variable(s) visible in the Variables section |
| 2 | Remove variable reference from instructions: delete the {{variable}} text | The variable reference is removed from the Instructions field |
| 3 | Verify the variable row disappears | The corresponding variable row is no longer shown in the Variables section |
| 4 | Click Save | Save completes successfully |
| 5 | Reload the page | The page reloads |
| 6 | Verify the removed variable is gone; remaining variables are intact | The removed variable is absent; all other variables are still present |

---

## Expected Final State

After reload, the variable removed from the Instructions field is absent from the Variables section, and all remaining variables are intact.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The removed variable does not appear after reload; remaining variables are preserved.

**Fail:**
- Any step produces an error or unexpected result.
- The removed variable reappears after reload, or remaining variables are lost.
