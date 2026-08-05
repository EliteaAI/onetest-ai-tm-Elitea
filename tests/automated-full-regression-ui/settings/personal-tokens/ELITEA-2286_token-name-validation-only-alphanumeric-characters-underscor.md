---
id: ELITEA-2286
title: "Token name validation — only alphanumeric characters, underscores, and hyphens are allowed"
priority: high
type: functional
module: settings-personal-tokens
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_personal_token_create_and_verify.TestPersonalTokenCreateAndVerify.test_invalid_token_name_shows_error_and_keeps_generate_disabled
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1178
---

# ELITEA-2286: Token name validation — only alphanumeric characters, underscores, and hyphens are allowed

**Module:** settings-personal-tokens · **Priority:** high · **Type:** functional

**Objective:** Verify that Token name validation — only alphanumeric characters, underscores, and hyphens are allowed. Success is confirmed when verify the "generate" button becomes enabled.

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
| 2 | Enter a token name with special characters (e.g., "my token!@#") | Field accepts the input and displays the entered value. |
| 3 | Verify a validation error is shown or invalid characters are rejected | Condition holds as described. |
| 4 | Verify the "Generate" button is disabled | Condition holds as described. |
| 5 | Clear the name and enter a name with a space (e.g., "my token") | Action completes without error and produces the expected UI state. |
| 6 | Verify the space is rejected or a validation error is shown | Condition holds as described. |
| 7 | Leave the token name field empty | Action completes without error and produces the expected UI state. |
| 8 | Verify the "Generate" button is disabled or an inline validation error is shown | Condition holds as described. |
| 9 | Clear the name and enter a valid name using only allowed characters: "my_token-123" | Action completes without error and produces the expected UI state. |
| 10 | Verify no validation error is shown | Condition holds as described. |
| 11 | Verify the "Generate" button becomes enabled | Condition holds as described. |

---

## Expected Final State

Verify the "Generate" button becomes enabled.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Token name validation — only alphanumeric characters, underscores, and hyphens are allowed.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
