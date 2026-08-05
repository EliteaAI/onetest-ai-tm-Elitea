---
id: ELITEA-2280
title: "Create a new personal token and verify it appears in the table"
priority: medium
type: functional
module: settings-personal-tokens
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_personal_token_create_and_verify.TestPersonalTokenCreateAndVerify.test_create_personal_token_and_verify_in_table
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1174
---

# ELITEA-2280: Create a new personal token and verify it appears in the table

**Module:** settings-personal-tokens · **Priority:** medium · **Type:** functional

**Objective:** Verify that Create a new personal token and verify it appears in the table. Success is confirmed when verify that token was copied to clipboard.

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
| 1 | Navigate to Settings → Personal Tokens | Target page/section loads successfully. |
| 2 | Click the "+" button | Control responds; expected next state is shown. |
| 3 | Verify a "New Token" form opens with: Name field and Expiration period (unit dropdown + numeric value) | Condition holds as described. |
| 4 | Enter token name "autotest-token" | Field accepts the input and displays the entered value. |
| 5 | Set expiration: unit "Days", value "30" | Action completes without error and produces the expected UI state. |
| 6 | Click "Generate" | Control responds; expected next state is shown. |
| 7 | Verify a "New token generated!" dialog appears | Condition holds as described. |
| 8 | Verify the dialog shows a warning: "This token will only be shown once, so make sure to copy and save it." | Condition holds as described. |
| 9 | Verify the token name is shown above the full token value in the dialog | Condition holds as described. |
| 10 | Verify a "Copy" button is present — click it and verify a success confirmation appears | Condition holds as described. |
| 11 | Close the dialog | Action completes without error and produces the expected UI state. |
| 12 | Verify "autotest-token" appears in the tokens table with masked value "...XXXX" | Condition holds as described. |
| 13 | Verify the Expiration column shows a green ✅ icon and "in 30 days" label | Condition holds as described. |
| 14 | Verify that token was copied to clipboard | Condition holds as described. |

---

## Expected Final State

Verify that token was copied to clipboard.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Create a new personal token and verify it appears in the table.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
