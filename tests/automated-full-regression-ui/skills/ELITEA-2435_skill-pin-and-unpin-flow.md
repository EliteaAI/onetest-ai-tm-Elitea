---
id: ELITEA-2435
title: "Skill pin and unpin flow"
priority: medium
type: functional
module: skills
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:skills]
requirements: []
---

# ELITEA-2435: Skill pin and unpin flow

**Module:** skills · **Priority:** medium · **Type:** functional

**Objective:** Verify that Skill pin and unpin flow. Success is confirmed when verify the skill is no longer marked as pinned.

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
| 1 | Navigate to the Skills list page and note which Skills (if any) are currently pinned | Target page/section loads successfully. |
| 2 | Open an existing unpinned Skill | Target page/section loads successfully. |
| 3 | Open the overflow (three-dot) menu | Target page/section loads successfully. |
| 4 | Verify the menu shows a "Pin" label/button | Condition holds as described. |
| 5 | Click "Pin" | Control responds; expected next state is shown. |
| 6 | Re-open the overflow menu | Action completes without error and produces the expected UI state. |
| 7 | Verify the menu now shows "Unpin" label/button (not "Pin") | Condition holds as described. |
| 8 | Navigate back to the Skills list page | Target page/section loads successfully. |
| 9 | Verify the pinned Skill is visually marked as pinned (e.g., pin icon, top of list, or pinned section) | Condition holds as described. |
| 10 | Re-open the same Skill | Action completes without error and produces the expected UI state. |
| 11 | Open the overflow menu and click "Unpin" | Target page/section loads successfully. |
| 12 | Re-open the overflow menu | Action completes without error and produces the expected UI state. |
| 13 | Verify the menu now shows "Pin" label/button again | Condition holds as described. |
| 14 | Navigate back to the Skills list page | Target page/section loads successfully. |
| 15 | Verify the Skill is no longer marked as pinned | Condition holds as described. |

---

## Expected Final State

Verify the Skill is no longer marked as pinned.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Skill pin and unpin flow.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
