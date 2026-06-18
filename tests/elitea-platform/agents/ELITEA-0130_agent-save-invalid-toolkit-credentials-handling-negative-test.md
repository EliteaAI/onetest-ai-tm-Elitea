---
id: ELITEA-0130
title: "Agent Save - Invalid Toolkit Credentials Handling (Negative Test)"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: []
requirements: []
---
# ELITEA-0130: Agent Save - Invalid Toolkit Credentials Handling (Negative Test)

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that saving an agent with a toolkit that has invalid credentials shows a validation error without losing changes or freezing the page.

## Preconditions

User logged into Elitea stage.elitea.ai\nA toolkit exists with invalid or expired credentials\nUser has permissions to create/edit agents

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create or open an existing agent for editing | Agent configuration form is displayed and editable |
| 2 | Make several changes to the agent: update name, modify instructions, change model settings | Changes are reflected in the form fields |
| 3 | Add a toolkit that has invalid or missing credentials | Toolkit is added to the agent's toolkit list |
| 4 | Click Save button | A validation error message is displayed indicating invalid toolkit credentials |
| 5 | Verify the page remains responsive (scroll, click fields, type text) | Page is fully interactive; no freezing or unresponsive state |
| 6 | Verify all previously made changes (name, instructions, model) are preserved in the form | All unsaved changes are still visible in the form fields |
| 7 | Check the browser developer console (F12 > Console) for unhandled exceptions or React error boundaries triggered by the save failure | No unhandled JavaScript exceptions or React error boundary crashes in the console — errors are caught and handled gracefully by the application |
| 8 | Add a second toolkit with valid credentials alongside the invalid one, then click Save again | Validation error still shown for the invalid toolkit — valid toolkit does not mask or bypass the invalid one. Both toolkits remain in the list |
| 9 | Remove the invalid toolkit and click Save again | Agent saves successfully with the valid toolkit and all other changes preserved |
| 10 | Reload the page and verify saved changes persisted | All changes (except the removed invalid toolkit) are persisted correctly — name, instructions, model settings, and valid toolkit are all present |
| 11 | Navigate to the embedded chat on the agent detail page and send a test message to verify the agent functions correctly with the valid toolkit | Agent responds successfully and can use the valid toolkit — the save failure for the invalid toolkit did not corrupt the agent's overall configuration |
| 12 | Re-add the invalid toolkit, attempt to save, then click the browser back button or navigate away without saving | Unsaved changes warning dialog appears (if applicable), or changes are discarded. Agent config returns to its last successfully saved state with the valid toolkit only |

## Expected Final State

Unsaved changes warning dialog appears (if applicable), or changes are discarded. Agent config returns to its last successfully saved state with the valid toolkit only

## Pass/Fail Criteria

Validation error message displayed (no silent failure)
Page remains responsive after save attempt
Form field values preserved (no data loss)
No unhandled JavaScript exceptions in browser console
Valid toolkit does not mask invalid toolkit validation
Successful save after removing invalid toolkit
Agent functions correctly with valid toolkit post-save
No browser console errors indicating crash
Navigation away from unsaved invalid state handled properly
