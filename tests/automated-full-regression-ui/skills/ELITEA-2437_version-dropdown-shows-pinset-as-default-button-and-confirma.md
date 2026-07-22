---
id: ELITEA-2437
title: "Version dropdown shows pin/set-as-default button and confirmation message"
priority: medium
type: functional
module: skills
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:skills]
requirements: []
---

# ELITEA-2437: Version dropdown shows pin/set-as-default button and confirmation message

**Module:** skills · **Priority:** medium · **Type:** functional

**Objective:** Verify that Version dropdown shows pin/set-as-default button and confirmation message. Success is confirmed when verify a confirmation message or indicator is shown.

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
| 1 | Open a Skill with multiple versions | Target page/section loads successfully. |
| 2 | Open the version selector dropdown | Target page/section loads successfully. |
| 3 | Verify each version row shows a pin/set-as-default control | Condition holds as described. |
| 4 | Click pin/set-as-default on a named version | Control responds; expected next state is shown. |
| 5 | Verify a confirmation message or indicator is shown | Condition holds as described. |

---

## Expected Final State

Verify a confirmation message or indicator is shown.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Version dropdown shows pin/set-as-default button and confirmation message.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
