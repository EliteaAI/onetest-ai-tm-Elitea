---
id: ELITEA-1912
title: "Build with AI — all generated draft fields are editable before approval"
priority: medium
type: functional
module: agents
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:agents]
requirements: []
automation_test_id:
  - tests.ui.agents.test_agent_build_with_ai.TestAgentBuildWithAIDraftFieldPopulation.test_edited_fields_persist_after_approve
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1319
---

# ELITEA-1912: Build with AI — all generated draft fields are editable before approval

**Module:** agents · **Priority:** medium · **Type:** functional

**Objective:** Verify that all fields in the generated agent draft review form (Name, Description, Instructions, Welcome message, Conversation starters) can be freely edited before approval, and the created agent reflects the edited values.

---

## Preconditions

- User is logged in to the Elitea platform with admin or editor role.
- An agent draft has been generated and the review/edit form is displayed.

---

## Test Data

| Field | Value |
|-------|-------|
| Edited Name | A valid unique name (different from generated) |
| Edited Description | A new description text |
| Edited Instructions | New instructions text |
| Edited Welcome message | New welcome message text |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Generate an agent draft and enter the review form | The review/edit form is displayed with all fields pre-populated |
| 2 | Edit the Name to a new valid value | The Name field accepts the new value and displays it |
| 3 | Edit the Description to a new value | The Description field accepts the new value |
| 4 | Edit the Instructions to a new value | The Instructions field accepts the new value |
| 5 | Edit the Welcome message to a new value | The Welcome message field accepts the new value |
| 6 | Edit or remove one of the Conversation starters | The Conversation starters field reflects the edit or removal |
| 7 | Click "Approve" / "Create Agent" | The agent creation is initiated with the edited values |
| 8 | Open the created Agent and verify all fields reflect the edited values (not the original generated values) | All fields (Name, Description, Instructions, Welcome message, Conversation starters) show the user-edited values |

---

## Expected Final State

The created agent stores all user-edited field values, confirming that pre-generation values were overridden by the user's edits before approval.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The created agent reflects all edited field values, not the original generated values.

**Fail:**
- Any step produces an error or unexpected result.
- Any field in the created agent shows the original generated value instead of the user-edited value.
