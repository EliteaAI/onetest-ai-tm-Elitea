---
id: ELITEA-1871
title: "Agent lifecycle: Create with validation, edit and persist, discard changes"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:agents]
requirements: []
---

# ELITEA-1871: Agent lifecycle: Create with validation, edit and persist, discard changes

**Module:** agents · **Priority:** critical · **Type:** functional

**Objective:** Verify the complete agent creation and editing lifecycle: that Save is only enabled when required fields are filled, that edits persist after save and reload, and that the Discard action properly reverts unsaved changes.

---

## Preconditions

- User is logged in to the Elitea platform.
- The Create Agent page is accessible.

---

## Test Data

| Field | Value |
|-------|-------|
| Agent Name | Test Lifecycle Agent |
| Agent Description | Agent for lifecycle testing |
| Initial Instructions | You are a test assistant. |
| Updated Instructions | You are an updated test assistant. |

---

## Steps

### Part 1: Create Agent with Field Validation

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Create Agent page | The Create Agent form is displayed with all fields empty |
| 2 | Fill only the Instructions field with "You are a test assistant." | Instructions field accepts input |
| 3 | Verify Save button is disabled | Save button remains disabled |
| 4 | Fill only Name field: "Test Lifecycle Agent" | Name field is filled; Save button remains disabled |
| 5 | Clear Name, fill only Description: "Agent for lifecycle testing" | Description field is filled; Save button remains disabled |
| 6 | Fill both Name and Description fields | Both fields are populated |
| 7 | Verify Save button becomes enabled | Save button becomes enabled (clickable) |
| 8 | Click Save | Agent is created successfully, page is refreshed and conversation appears. Name of just created agent is displayed in breadcrumbs |

### Part 2: Edit Instructions and Verify Persistence

| # | Action | Expected Result |
|---|--------|-----------------|
| 9 | Open the newly created agent's detail page | The agent detail page loads with current values |
| 10 | Switch the Instructions section to Edit mode if it is in Preview (agent detail page opens in Preview), then clear the Instructions field and enter: "You are an updated test assistant." | The Instructions field displays the new text |
| 11 | Click Save and wait for network idle | Save completes successfully; confirmation is shown or save button returns to default state |
| 12 | Reload the page | The page reloads |
| 13 | Verify Instructions field contains "You are an updated test assistant." | The Instructions field displays the saved text |

### Part 3: Discard Changes and Verify Revert

| # | Action | Expected Result |
|---|--------|-----------------|
| 14 | Switch Instructions to Edit mode if in Preview, then modify Name to "Modified Name", Description to "Modified Description", and Instructions to "Modified instructions" | All three fields display new unsaved values |
| 15 | Click the Discard button (or navigate away and confirm discard) | Discard action is triggered; any confirmation dialog is accepted |
| 16 | Verify all three fields reverted to their previously saved values | Name: "Test Lifecycle Agent", Description: "Agent for lifecycle testing", Instructions: "You are an updated test assistant." |

---

## Expected Final State

- Agent exists with Name "Test Lifecycle Agent", Description "Agent for lifecycle testing", Instructions "You are an updated test assistant."
- All unsaved modifications were successfully discarded and fields show saved values.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Save button enables only when both Name and Description are filled during creation.
- Instructions persist correctly after save and reload.
- Discard action reverts all three fields to their previously saved values.

**Fail:**
- Any step produces an error or unexpected result.
- Save button behavior is incorrect (enables too early or remains disabled when it should enable).
- Instructions do not persist after reload.
- Discard fails to revert fields or reverts them incorrectly.

---

## Notes

**Source functional tests:** ELITEA-1871, ELITEA-1872, ELITEA-1873

**Regression rationale:** Consolidates the critical agent creation, editing, and discard workflow into a single end-to-end test. All key validations and checkpoints from the original three tests are preserved:
- ELITEA-1871: Save button validation during creation
- ELITEA-1872: Edit persistence after reload
- ELITEA-1873: Discard functionality

**Selected checkpoints:**
- Save button state validation (disabled/enabled based on required fields)
- Successful agent creation
- Instruction editing and persistence verification
- Multi-field discard and revert verification
