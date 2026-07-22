---
id: ELITEA-2427
title: "History session shows correct preview and title"
priority: medium
type: functional
module: support-assistant
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:support-assistant]
requirements: []
---

# ELITEA-2427: History session shows correct preview and title

**Module:** support-assistant · **Priority:** medium · **Type:** functional

**Objective:** Verify that History session shows correct preview and title. Success is confirmed when verify the history entry shows a short preview of the conversation content ------ issue 5723 is assigned for current release----.

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
| 1 | Open the Support Assistant widget | Target page/section loads successfully. |
| 2 | Send the distinctive message "HISTORY-TITLE-TEST: Tell me about ELITEA" | Action completes without error and produces the expected UI state. |
| 3 | Wait for the assistant response | Wait completes; subsequent state is ready. |
| 4 | Click New Chat to push the session into history | Control responds; expected next state is shown. |
| 5 | Open the History panel | Target page/section loads successfully. |
| 6 | Verify the most recent history entry shows a recognizable label — either the first user message text ("HISTORY-TITLE-TEST…") or a generated title derived from the conversation | Condition holds as described. |
| 7 | Verify the history entry shows a timestamp or date indicator | Condition holds as described. |
| 8 | Verify the history entry shows a short preview of the conversation content ------ Issue 5723 is assigned for current release---- | Condition holds as described. |

---

## Expected Final State

Verify the history entry shows a short preview of the conversation content ------ Issue 5723 is assigned for current release----.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: History session shows correct preview and title.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
