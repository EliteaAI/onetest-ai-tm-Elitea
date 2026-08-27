---
id: ELITEA-2346
title: "Hidden secret does not appear in secret selection dropdown for new credentials"
priority: medium
type: functional
module: settings-secrets
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_hidden_secret_absent_from_ai_provider_dropdown.TestHiddenSecretAbsentFromAIProviderDropdown.test_hidden_secret_absent_from_ai_provider_dropdown
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1912"
---

# ELITEA-2346: Hidden secret does not appear in secret selection dropdown for new credentials

**Module:** settings-secrets · **Priority:** medium · **Type:** functional

**Objective:** Verify that Hidden secret does not appear in secret selection dropdown for new credentials. Success is confirmed when verify "autotest_secret" does not appear in the dropdown list.

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
| 1 | Navigate to Settings → Secrets and hide a secret (e.g., "autotest_secret") | Target page/section loads successfully. |
| 2 | Navigate to Settings → AI Configuration → click "+" to create a new model configuration | Target page/section loads successfully. |
| 3 | Open the secret/credentials selection dropdown | Target page/section loads successfully. |
| 4 | Verify "autotest_secret" does NOT appear in the dropdown list | Condition holds as described. |

---

## Expected Final State

Verify "autotest_secret" does NOT appear in the dropdown list.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Hidden secret does not appear in secret selection dropdown for new credentials.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
