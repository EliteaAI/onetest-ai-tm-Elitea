---
id: ELITEA-1870
title: "Agent listing — \"+Create\" button navigates to Create Agent page"
priority: critical
type: functional
module: agents
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:agents]
requirements: []
automation_test_id: tests.ui.agents.test_agent_create_button_navigation.test_create_button_navigates_to_create_agent_page
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/547
---

# ELITEA-1870: Agent listing — "+Create" button navigates to Create Agent page

**Module:** agents · **Priority:** high · **Type:** functional

**Objective:** Verify that clicking the "+ Create" button on the Agents dashboard navigates to the Create Agent page with an empty form and the Save button disabled by default.

---

## Preconditions

- User is logged in to the Elitea platform.

---

## Test Data

| Field | Value |
|-------|-------|
| Target URL | /agents/all |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Agents dashboard (/agents/all) | The Agents dashboard loads correctly |
| 2 | Click the "+ Create" button | Browser navigates to the Create Agent page |
| 3 | Verify the browser navigates to /agents/create (or equivalent) | The URL reflects the create agent route |
| 4 | Verify the Create Agent form is shown with empty Name, Description, and Instructions fields | All three fields are empty |
| 5 | Verify the Save button is disabled by default | Save button is disabled (not clickable) |

---

## Expected Final State

The Create Agent form is displayed with empty Name, Description, and Instructions fields, and the Save button is disabled.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The Create Agent form loads with empty fields and a disabled Save button.

**Fail:**
- Any step produces an error or unexpected result.
- The form is not shown, fields are pre-filled, or the Save button is enabled without input.
