---
id: ELITEA-2464
title: "Chat – Modules panel accessible from + icon in conversation with all toggles functional"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2464: Chat – Modules panel accessible from + icon in conversation with all toggles functional

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that Chat – Modules panel accessible from + icon in conversation with all toggles functional. Success is confirmed when close the modules panel and verify the main conversation view is restored.

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
| 1 | Navigate to the Chats section and open any existing conversation | Target page/section loads successfully. |
| 2 | Click the + icon at the bottom left of the message input area | Control responds; expected next state is shown. |
| 3 | Verify a popup menu appears with options: Attach Files, Modules, Agents, Pipelines, Toolkits, MCPs | Condition holds as described. |
| 4 | Click Modules | Control responds; expected next state is shown. |
| 5 | Verify the Modules panel opens showing toggleable features: Image creation, Data Analysis, Agents & Pipeline Builder, Planner, Python Sandbox, Swarm Mode, Smart Tool Selection | Condition holds as described. |
| 6 | Verify each toggle displays its current on/off state | Condition holds as described. |
| 7 | Click the toggle for each module one by one switching on and off | Control responds; expected next state is shown. |
| 8 | Verify the state changes correctly for each toggle | Condition holds as described. |
| 9 | Verify a "Modules configuration Updated" success message appears after each toggle change | Condition holds as described. |
| 10 | Verify no error messages are shown | Condition holds as described. |
| 11 | Close the Modules panel and verify the main conversation view is restored | Action completes without error and produces the expected UI state. |

---

## Expected Final State

Close the Modules panel and verify the main conversation view is restored.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Chat – Modules panel accessible from + icon in conversation with all toggles functional.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
