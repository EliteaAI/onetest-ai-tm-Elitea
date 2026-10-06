---
id: ELITEA-2382
title: "Default User Instructions text persists after save and reload"
priority: medium
type: functional
module: settings-user-profile
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2382: Default User Instructions text persists after save and reload

**Module:** settings-user-profile · **Priority:** medium · **Type:** functional

**Objective:** Verify that Default User Instructions text persists after save and reload. Success is confirmed when verify the default user instructions field shows the entered text.

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
| 1 | Navigate to Personalization → GENERAL section | Target page/section loads successfully. |
| 2 | Click the Default User Instructions textarea | Control responds; expected next state is shown. |
| 3 | Enter: "Always respond in a concise manner. Focus on practical solutions." | Field accepts the input and displays the entered value. |
| 4 | Click outside to trigger autosave | Control responds; expected next state is shown. |
| 5 | Reload the page | Action completes without error and produces the expected UI state. |
| 6 | Verify the Default User Instructions field shows the entered text | Condition holds as described. |

---

## Expected Final State

Verify the Default User Instructions field shows the entered text.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Default User Instructions text persists after save and reload.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
