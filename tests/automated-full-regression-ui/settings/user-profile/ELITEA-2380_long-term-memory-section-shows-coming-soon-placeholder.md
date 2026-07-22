---
id: ELITEA-2380
title: "Long-term memory section shows \"Coming soon\" placeholder"
priority: medium
type: functional
module: settings-user-profile
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2380: Long-term memory section shows \"Coming soon\" placeholder

**Module:** settings-user-profile · **Priority:** medium · **Type:** functional

**Objective:** Verify that Long-term memory section shows "Coming soon" placeholder. Success is confirmed when verify no error state is shown.

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
| 1 | Navigate to Personalization → LONG-TERM MEMORY section | Target page/section loads successfully. |
| 2 | Verify the section is visible and expandable | Condition holds as described. |
| 3 | Verify the content shows a "Coming soon" message about managing what the AI remembers across conversations | Condition holds as described. |
| 4 | Verify no interactive controls (inputs, toggles, buttons) are present in this section | Condition holds as described. |
| 5 | Verify no error state is shown | Condition holds as described. |

---

## Expected Final State

Verify no error state is shown.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Long-term memory section shows "Coming soon" placeholder.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
