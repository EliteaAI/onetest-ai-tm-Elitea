---
id: ELITEA-2343
title: "Eye icon reveals the actual secret value and changes to crossed-out eye"
priority: medium
type: functional
module: settings-secrets
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_secret_eye_icon_reveal_and_mask_toggle.TestSecretEyeIconRevealAndMaskToggle.test_secret_eye_icon_reveal_and_mask_toggle
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1225
---

# ELITEA-2343: Eye icon reveals the actual secret value and changes to crossed-out eye

**Module:** settings-secrets · **Priority:** medium · **Type:** functional

**Objective:** Verify that Eye icon reveals the actual secret value and changes to crossed-out eye. Success is confirmed when verify the icon reverts to the normal eye icon.

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
| 1 | Navigate to Settings → Secrets | Target page/section loads successfully. |
| 2 | Locate any secret row showing a masked "{{secret.name}}" value | Action completes without error and produces the expected UI state. |
| 3 | Click the eye icon on that row | Control responds; expected next state is shown. |
| 4 | Verify the Value column updates to show the actual secret value (plaintext) | Condition holds as described. |
| 5 | Verify the eye icon changes to a crossed-out eye icon | Condition holds as described. |
| 6 | Click the crossed-out eye icon | Control responds; expected next state is shown. |
| 7 | Verify the value returns to the masked "{{secret.name}}" format | Condition holds as described. |
| 8 | Verify the icon reverts to the normal eye icon | Condition holds as described. |

---

## Expected Final State

Verify the icon reverts to the normal eye icon.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Eye icon reveals the actual secret value and changes to crossed-out eye.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
