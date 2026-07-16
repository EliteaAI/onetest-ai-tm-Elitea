---
id: ELITEA-1872
title: "Edit agent instructions and verify persistence"
priority: critical
type: functional
module: agents
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:agents]
requirements: []
automation_test_id: tests.ui.agents.test_agent_management.TestAgentActions.test_edit_agent_instructions
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/540
---

# ELITEA-1872: Edit agent instructions and verify persistence

**Module:** agents · **Priority:** high · **Type:** functional

**Objective:** Verify that changes to the Instructions field are saved correctly and persist after a page reload.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing agent is available in the current project.

---

## Test Data

| Field | Value |
|-------|-------|
| New instructions | You are an updated test assistant. |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to an existing agent's detail page | The agent detail page loads with current field values |
| 2 | Clear the Instructions field and enter new instructions: "You are an updated test assistant." | The Instructions field displays the new text |
| 3 | Click Save and wait for network idle | Save completes successfully; confirmation is shown or save button returns to default state |
| 4 | Reload the page | The page reloads |
| 5 | Verify the Instructions field contains "You are an updated test assistant." | The Instructions field displays the saved text |

---

## Expected Final State

After reload, the Instructions field contains "You are an updated test assistant.", confirming the change was persisted.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Instructions field retains the new value after page reload.

**Fail:**
- Any step produces an error or unexpected result.
- The Instructions field reverts to its previous value or shows a different value after reload.
