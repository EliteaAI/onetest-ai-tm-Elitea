---
id: ELITEA-2336
title: "Create secret inline — \"+\" adds editable row, checkmark saves, X cancels"
priority: medium
type: functional
module: settings-secrets
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_secret_create_inline_checkmark_x_cancel.TestSecretCreateInlineCheckmarkXCancel.test_create_secret_inline_checkmark_saves_x_cancels
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1205
---

# ELITEA-2336: Create secret inline — \"+\" adds editable row, checkmark saves, X cancels

**Module:** settings-secrets · **Priority:** medium · **Type:** functional

**Objective:** Verify that Create secret inline — "+" adds editable row, checkmark saves, X cancels. Success is confirmed when verify the row is discarded and no secret is created.

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
| 2 | Click the "+" button | Control responds; expected next state is shown. |
| 3 | Verify a new inline editable row appears at the current pagination position (not a modal/dialog) | Condition holds as described. |
| 4 | Enter name "autotest_secret" and value "my-secret-value-123" | Field accepts the input and displays the entered value. |
| 5 | Click the ✓ (checkmark) icon | Control responds; expected next state is shown. |
| 6 | Verify the row saves and shows "autotest_secret" with masked "{{secret.autotest_secret}}" value | Condition holds as described. |
| 7 | Click "+" again — enter any name and value | Control responds; expected next state is shown. |
| 8 | Click the ✗ (close/cancel) icon | Control responds; expected next state is shown. |
| 9 | Verify the row is discarded and no secret is created | Condition holds as described. |

---

## Expected Final State

Verify the row is discarded and no secret is created.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Create secret inline — "+" adds editable row, checkmark saves, X cancels.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
