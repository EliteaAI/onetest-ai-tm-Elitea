---
id: ELITEA-2288
title: "Duplicate token names are allowed"
priority: medium
type: functional
module: settings-personal-tokens
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_personal_token_duplicate_names.TestPersonalTokenDuplicateNames.test_duplicate_token_names_are_allowed
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1900"
---

# ELITEA-2288: Duplicate token names are allowed

**Module:** settings-personal-tokens · **Priority:** medium · **Type:** functional

**Objective:** Verify that Duplicate token names are allowed. Success is confirmed when verify each token has a distinct masked token value.

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
| 2 | Create a token with name "duplicate-test" | Operation completes successfully; state updates and confirmation is shown. |
| 3 | Create a second token with the same name "duplicate-test" | Operation completes successfully; state updates and confirmation is shown. |
| 4 | Verify both tokens appear in the table without error | Condition holds as described. |
| 5 | Verify each token has a distinct masked token value | Condition holds as described. |

---

## Expected Final State

Verify each token has a distinct masked token value.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Duplicate token names are allowed.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
