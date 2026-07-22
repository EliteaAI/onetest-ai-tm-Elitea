---
id: ELITEA-2359
title: "Agent Hub — copy link from agent detail modal navigates to agent"
priority: medium
type: functional
module: agent-hub
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:agent-hub]
requirements: []
---

# ELITEA-2359: Agent Hub — copy link from agent detail modal navigates to agent

**Module:** agent-hub · **Priority:** medium · **Type:** functional

**Objective:** Verify that Agent Hub — copy link from agent detail modal navigates to agent. Success is confirmed when verify all agent details (name, description, conversation starters, welcome message) are displayed correctly.

---

## Preconditions

- User is logged in to the Elitea platform.


---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Agent Hub | Target page/section loads successfully. |
| 2 | Click on any agent card to open the detail modal | Control responds; expected next state is shown. |
| 3 | Click the link/copy icon button in the modal header | Control responds; expected next state is shown. |
| 4 | Verify a success notification appears (e.g., "Link has been copied to the clipboard") | Condition holds as described. |
| 5 | Open a new browser tab and paste the copied URL into the address bar | Target page/section loads successfully. |
| 6 | Navigate to the pasted URL | Target page/section loads successfully. |
| 7 | Verify the correct agent detail modal opens directly | Condition holds as described. |
| 8 | Verify all agent details (name, description, conversation starters, welcome message) are displayed correctly | Condition holds as described. |

---

## Expected Final State

Verify all agent details (name, description, conversation starters, welcome message) are displayed correctly.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Agent Hub — copy link from agent detail modal navigates to agent.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
