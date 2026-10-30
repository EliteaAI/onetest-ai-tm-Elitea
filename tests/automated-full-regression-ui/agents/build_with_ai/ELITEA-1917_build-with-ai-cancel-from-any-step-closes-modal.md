---
id: ELITEA-1917
title: "Build with AI — Cancel from any step closes modal without creating an agent"
priority: medium
type: functional
module: agents
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:agents]
requirements: []
---

# ELITEA-1917: Build with AI — Cancel from any step closes modal without creating an agent

**Module:** agents · **Priority:** medium · **Type:** functional

**Objective:** Verify that clicking Cancel at any point in the GenerateAgentModal workflow (prompt input step or review step) closes the modal without creating an agent, and the New Agent form remains in its untouched state.

---

## Preconditions

- User is logged in to the Elitea platform with admin or editor role.
- The GenerateAgentModal is accessible from the New Agent creation page.

---

## Test Data

| Field | Value |
|-------|-------|
| Natural-language prompt | Any description text (not submitted or partially reviewed) |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the GenerateAgentModal and enter a natural-language description in the prompt input step | The input field contains the entered text |
| 2 | Click "Cancel" without generating | The Cancel action is triggered |
| 3 | Verify the modal closes | The GenerateAgentModal is closed and no longer visible |
| 4 | Verify the New Agent form is still shown with empty/untouched fields | The New Agent creation form is displayed with fields in their original empty/untouched state |
| 5 | Verify no new Agent was created in the Agents list | Navigating to the Agents list shows no new agent was added |
| 6 | Open the GenerateAgentModal again and enter a description | The modal opens and description is entered |
| 7 | Click "Generate agent" and wait for the review form to appear | The review form is displayed with generated draft fields |
| 8 | Click "Cancel" from the review step | The Cancel action is triggered |
| 9 | Verify the modal closes | The GenerateAgentModal is closed and no longer visible |
| 10 | Verify the New Agent form is still shown with empty/untouched fields | The New Agent creation form is displayed in its original state |
| 11 | Verify no new Agent was created in the Agents list | Navigating to the Agents list shows no new agent was added |

---

## Expected Final State

The modal closes after Cancel from either the prompt input step or the review step, the New Agent form remains unmodified, and no agent is created.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Cancel from prompt step: modal closes, form untouched, no agent created.
- Cancel from review step: modal closes, form untouched, no agent created.

**Fail:**
- Any step produces an error or unexpected result.
- The modal does not close after Cancel.
- The New Agent form is modified unexpectedly.
- A new agent appears in the Agents list after Cancel.

---

## Notes

**Source functional tests:** ELITEA-1917 (original), ELITEA-1918 (original)  
**Regression rationale:** Consolidated test verifying Cancel behavior from both modal steps (prompt input and review). Both test the same core assertion: Cancel closes the modal without creating an agent or modifying the form. Testing both steps ensures the Cancel button works consistently across the modal workflow.  
**Selected checkpoints:** Modal closure, form state preservation, no agent creation (from both steps).
