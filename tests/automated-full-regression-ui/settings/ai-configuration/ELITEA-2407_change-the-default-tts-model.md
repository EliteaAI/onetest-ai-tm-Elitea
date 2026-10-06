---
id: ELITEA-2407
title: "Change the default TTS model"
priority: medium
type: functional
module: settings-ai-configuration
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2407: Change the default TTS model

**Module:** settings-ai-configuration · **Priority:** medium · **Type:** functional

**Objective:** Verify that Change the default TTS model. Success is confirmed when verify the previously default card no longer shows the "default" badge.

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
| 1 | Navigate to Settings → AI Configuration → Text to Speech (TTS) section | Target page/section loads successfully. |
| 2 | Note the currently selected default TTS model | Action completes without error and produces the expected UI state. |
| 3 | Click the "Default TTS model" dropdown and select a different model | Control responds; expected next state is shown. |
| 4 | Verify the selector updates to reflect the new selection | Condition holds as described. |
| 5 | Verify the selected model card gains a "Default" badge | Condition holds as described. |
| 6 | Verify the previously default card no longer shows the "Default" badge | Condition holds as described. |

---

## Expected Final State

Verify the previously default card no longer shows the "Default" badge.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Change the default TTS model.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
