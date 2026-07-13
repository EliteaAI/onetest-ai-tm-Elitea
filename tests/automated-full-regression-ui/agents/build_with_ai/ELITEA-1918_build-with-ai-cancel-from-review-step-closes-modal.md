---
id: ELITEA-1918
title: "Build with AI — Cancel from review step closes modal without creating an agent"
priority: medium
type: functional
module: agents
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:agents]
requirements: []
---

# ELITEA-1918: Build with AI — Cancel from review step closes modal without creating an agent

**Module:** agents · **Priority:** medium · **Type:** functional

**Objective:** Verify that clicking Cancel on the review/edit step of the GenerateAgentModal closes the modal without creating an agent.

---

## Preconditions

- User is logged in to the Elitea platform with admin or editor role.
- An agent draft has been generated and the review/edit form is displayed.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Generate an agent draft and reach the review/edit form | The review/edit form is displayed with draft data |
| 2 | Click "Cancel" | The Cancel action is triggered |
| 3 | Verify the modal closes | The GenerateAgentModal is closed and no longer visible |
| 4 | Verify no Agent was created in the Agents list | Navigating to the Agents list shows no new agent was added |

---

## Expected Final State

The modal is closed and no agent was created in the project.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Modal closes and no agent is created.

**Fail:**
- Any step produces an error or unexpected result.
- The modal does not close, or a new agent appears in the Agents list.
