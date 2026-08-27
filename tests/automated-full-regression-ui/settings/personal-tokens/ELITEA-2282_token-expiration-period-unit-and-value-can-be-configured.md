---
id: ELITEA-2282
title: "Token expiration period unit and value can be configured"
priority: medium
type: functional
module: settings-personal-tokens
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_personal_token_expiration_config.TestPersonalTokenExpirationConfig.test_token_expiration_unit_and_value_can_be_configured
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1900"
---

# ELITEA-2282: Token expiration period unit and value can be configured

**Module:** settings-personal-tokens · **Priority:** medium · **Type:** functional

**Objective:** Verify that Token expiration period unit and value can be configured. Success is confirmed when verify the expiration column shows a green ✅ icon and "in 7 days" label.

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
| 1 | Navigate to Settings → Personal Tokens and click "+" | Target page/section loads successfully. |
| 2 | Verify the Expiration period field has two parts: a unit dropdown and a numeric value input | Condition holds as described. |
| 3 | Click the unit dropdown — verify available options include at least: Days, Weeks, Hours, Minutes and Never | Control responds; expected next state is shown. |
| 4 | Select "Days" and enter value "7" | Control responds; expected next state is shown. |
| 5 | Click "Generate" and close the dialog | Control responds; expected next state is shown. |
| 6 | Verify the Expiration column shows a green ✅ icon and "in 7 days" label | Condition holds as described. |

---

## Expected Final State

Verify the Expiration column shows a green ✅ icon and "in 7 days" label.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Token expiration period unit and value can be configured.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
