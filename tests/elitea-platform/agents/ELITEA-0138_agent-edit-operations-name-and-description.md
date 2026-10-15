---
id: ELITEA-0138
title: "Agent Edit Operations - Name and Description"
priority: high
type: functional
module: agents
status: ready
execution_type: manual
automation_test_id: []
tags: []
requirements: []
---
# ELITEA-0138: Agent Edit Operations - Name and Description

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify agent editing functionality: update name and description fields.

**Coverage:**
- Edit agent name
- Edit agent description

## Preconditions

- User is logged in to {{base_url}} via Keycloak
- At least one agent exists (create one manually if needed)
- Browser: Chrome or Chromium

## Test Data

- URL: {{base_url}}
- New name to test: autotest_renamed_agent
- New description to test: Updated description by automation

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agents from the sidebar. Open any existing agent to view its detail page. Wait for the form to fully load (the Name field should show the current name). | Agent detail page loads with the current name displayed in the Name field. |
| 2 | Click on the Name field, select all text (Ctrl+A), and type the new name 'autotest_renamed_agent'. | The Name field shows the updated value. The Save button becomes enabled. |
| 3 | Click the Save button. Wait for the save to complete. | The save operation completes successfully. |
| 4 | Reload the page (F5 or browser refresh). Wait for the form to load again. Check the Name field. | The Name field shows 'autotest_renamed_agent' — the change persisted after reload. |
| 5 | Click on the Description field, select all text, and type 'Updated description by automation'. | The Description field shows the updated value. |
| 6 | Click Save, then reload the page. Verify the Description field still shows the new value. | The Description field shows 'Updated description by automation' after reload. |

## Expected Final State

The Description field shows 'Updated description by automation' after reload.

## Pass/Fail Criteria

**Pass:**
- Name edit persists after save + reload
- Description edit persists after save + reload
- Save button enables after field changes
- MUI form correctly triggers React onChange via click+type

**Fail:**
- Name reverts after reload (not saved)
- Description reverts after reload
- Save button stays disabled after edits
- Form field doesn't accept input (fill() vs click+type issue)
