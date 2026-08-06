---
id: ELITEA-2344
title: "Hide option permanently removes the secret from the Secrets table"
priority: medium
type: functional
module: settings-secrets
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_secret_hide_via_three_dot_menu.TestSecretHideViaThreeDotMenu.test_hide_secret_via_three_dot_menu
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1228
---

# ELITEA-2344: Hide option permanently removes the secret from the Secrets table

**Module:** settings-secrets · **Priority:** medium · **Type:** functional

**Objective:** Verify that Hide option permanently removes the secret from the Secrets table. Success is confirmed when verify the "+" button is available to create a new secret with the same name if needed.

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
| 2 | Note the name of the secret to be hidden (e.g., "autotest_secret") | Action completes without error and produces the expected UI state. |
| 3 | Click the three-dot menu on that secret row | Control responds; expected next state is shown. |
| 4 | Click "Hide" | Control responds; expected next state is shown. |
| 5 | Verify a confirmation warning is shown stating: "Once hidden, the secret is completely removed from the Secrets table and will no longer be visible in the UI. Hidden secrets cannot be unhidden." | Condition holds as described. |
| 6 | Confirm the action | Operation completes successfully; state updates and confirmation is shown. |
| 7 | Verify the secret is no longer visible in the Secrets table | Condition holds as described. |
| 8 | Reload the page — verify the secret does not reappear | Action completes without error and produces the expected UI state. |
| 9 | Verify the "+" button is available to create a new secret with the same name if needed | Condition holds as described. |

---

## Expected Final State

Verify the "+" button is available to create a new secret with the same name if needed.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Hide option permanently removes the secret from the Secrets table.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
