---
id: ELITEA-2281
title: "Delete a personal token and verify it is removed from the table"
priority: medium
type: functional
module: settings-personal-tokens
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_personal_token_delete.TestPersonalTokenDelete.test_delete_personal_token_removed_from_table
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1900"
---

# ELITEA-2281: Delete a personal token and verify it is removed from the table

**Module:** settings-personal-tokens · **Priority:** medium · **Type:** functional

**Objective:** Verify that Delete a personal token and verify it is removed from the table. Success is confirmed when reload the page — verify the deleted token does not reappear.

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
| 2 | Locate an existing token in the table | Action completes without error and produces the expected UI state. |
| 3 | Click the trash icon in the Actions column | Control responds; expected next state is shown. |
| 4 | Verify a confirmation dialog appears | Condition holds as described. |
| 5 | Confirm deletion | Operation completes successfully; state updates and confirmation is shown. |
| 6 | Verify the token is removed from the table | Condition holds as described. |
| 7 | Reload the page — verify the deleted token does not reappear | Action completes without error and produces the expected UI state. |

---

## Expected Final State

Reload the page — verify the deleted token does not reappear.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Delete a personal token and verify it is removed from the table.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
