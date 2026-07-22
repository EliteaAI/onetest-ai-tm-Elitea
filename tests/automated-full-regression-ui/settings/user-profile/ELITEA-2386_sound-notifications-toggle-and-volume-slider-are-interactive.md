---
id: ELITEA-2386
title: "Sound Notifications — toggle and volume slider are interactive"
priority: medium
type: functional
module: settings-user-profile
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2386: Sound Notifications — toggle and volume slider are interactive

**Module:** settings-user-profile · **Priority:** medium · **Type:** functional

**Objective:** Verify that Sound Notifications — toggle and volume slider are interactive. Success is confirmed when verify "preview sound" is clickable.

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
| 1 | Navigate to Personalization → SOUND NOTIFICATIONS section | Target page/section loads successfully. |
| 2 | Verify "Play sound when tasks complete" toggle is present | Condition holds as described. |
| 3 | Verify the Volume slider is present with range 0% to 100% | Condition holds as described. |
| 4 | Toggle "Play sound when tasks complete" OFF | Action completes without error and produces the expected UI state. |
| 5 | Verify the Volume slider is disabled or hidden | Condition holds as described. |
| 6 | Toggle back ON — verify the Volume slider is re-enabled | Action completes without error and produces the expected UI state. |
| 7 | Verify "Preview Sound" is clickable | Condition holds as described. |

---

## Expected Final State

Verify "Preview Sound" is clickable.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Sound Notifications — toggle and volume slider are interactive.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
