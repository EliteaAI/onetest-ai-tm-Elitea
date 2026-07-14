---
id: ELITEA-1917
title: "Build with AI — Cancel from prompt step closes modal without creating an agent"
priority: medium
type: functional
module: agents
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:agents]
requirements: []
---

# ELITEA-1917: Build with AI — Cancel from prompt step closes modal without creating an agent

**Module:** agents · **Priority:** medium · **Type:** functional

**Objective:** Verify that clicking Cancel on the prompt input step of the GenerateAgentModal closes the modal without creating an agent, and the New Agent form remains in its untouched state.

---

## Preconditions

- User is logged in to the Elitea platform with admin or editor role.
- The GenerateAgentModal is open on the prompt input step.

---

## Test Data

| Field | Value |
|-------|-------|
| Natural-language prompt | Any description text (not submitted) |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the GenerateAgentModal and enter a natural-language description | The input field contains the entered text |
| 2 | Click "Cancel" without generating | The Cancel action is triggered |
| 3 | Verify the modal closes | The GenerateAgentModal is closed and no longer visible |
| 4 | Verify the New Agent form is still shown with empty/untouched fields | The New Agent creation form is displayed with fields in their original empty/untouched state |
| 5 | Verify no new Agent was created in the Agents list | Navigating to the Agents list shows no new agent was added |

---

## Expected Final State

The modal is closed, the New Agent form is unmodified, and no agent was created.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Modal closes, New Agent form is untouched, and no agent is created.

**Fail:**
- Any step produces an error or unexpected result.
- The modal does not close, the New Agent form is modified, or a new agent appears in the Agents list.
