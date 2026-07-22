---
id: ELITEA-2385
title: "Voice Personalization — Voice dropdown, Speed and Volume sliders are interactive"
priority: medium
type: functional
module: settings-user-profile
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2385: Voice Personalization — Voice dropdown, Speed and Volume sliders are interactive

**Module:** settings-user-profile · **Priority:** medium · **Type:** functional

**Objective:** Verify that Voice Personalization — Voice dropdown, Speed and Volume sliders are interactive. Success is confirmed when verify "preview voice" is clickable.

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
| 1 | Navigate to Personalization → VOICE PERSONALIZATION section | Target page/section loads successfully. |
| 2 | Verify the Voice dropdown is present and shows a selected option | Condition holds as described. |
| 3 | Click the Voice dropdown — verify a list of voice options appears | Control responds; expected next state is shown. |
| 4 | Select a different voice | Control responds; expected next state is shown. |
| 5 | Verify the Speed slider is present with range 0.5x to 2x | Condition holds as described. |
| 6 | Drag the Speed slider to 1.5x | Action completes without error and produces the expected UI state. |
| 7 | Verify the Volume slider is present with range Mute to 100% | Condition holds as described. |
| 8 | Drag the Volume slider to 50% | Action completes without error and produces the expected UI state. |
| 9 | Verify "Preview Voice" is clickable | Condition holds as described. |

---

## Expected Final State

Verify "Preview Voice" is clickable.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Voice Personalization — Voice dropdown, Speed and Volume sliders are interactive.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
