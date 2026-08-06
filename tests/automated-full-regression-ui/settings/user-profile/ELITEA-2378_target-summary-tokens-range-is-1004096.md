---
id: ELITEA-2378
title: "Target Summary Tokens range is 100–4096"
priority: medium
type: functional
module: settings-user-profile
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.settings.test_context_management_toggle.TestContextManagementToggle.test_target_summary_tokens_range_validation
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1246
---

# ELITEA-2378: Target Summary Tokens range is 100–4096

**Module:** settings-user-profile · **Priority:** medium · **Type:** functional

**Objective:** Verify that Target Summary Tokens range is 100–4096. Success is confirmed when verify no validation error is shown and save is enabled.

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
| 1 | Navigate to Personalization → DEFAULT SUMMARIZATION | Target page/section loads successfully. |
| 2 | Set Target Summary Tokens to 99 | Action completes without error and produces the expected UI state. |
| 3 | Verify a validation error is shown (value below minimum of 100) | Condition holds as described. |
| 4 | Set Target Summary Tokens to 4097 | Action completes without error and produces the expected UI state. |
| 5 | Verify a validation error is shown (value above maximum of 4096) | Condition holds as described. |
| 6 | Set Target Summary Tokens to 200 | Action completes without error and produces the expected UI state. |
| 7 | Verify no validation error is shown and Save is enabled | Condition holds as described. |

---

## Expected Final State

Verify no validation error is shown and Save is enabled.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Target Summary Tokens range is 100–4096.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
