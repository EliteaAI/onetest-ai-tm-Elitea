---
id: ELITEA-2345
title: "Hiding a secret used by existing credentials does not break those credentials"
priority: high
type: functional
module: settings-secrets
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_hidden_secret_not_breaking_credentials.TestHiddenSecretNotBreakingCredentials.test_hiding_secret_used_by_credential_does_not_break_it
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1912"
---

# ELITEA-2345: Hiding a secret used by existing credentials does not break those credentials

**Module:** settings-secrets · **Priority:** high · **Type:** functional

**Objective:** Verify that Hiding a secret used by existing credentials does not break those credentials. Success is confirmed when verify the hidden secret no longer appears in the secret selection dropdown when creating or editing a new credential.

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
| 2 | Identify a secret that is currently referenced by at least one credential | Action completes without error and produces the expected UI state. |
| 3 | Click the three-dot menu → Hide and confirm | Control responds; expected next state is shown. |
| 4 | Verify the secret is removed from the Secrets table | Condition holds as described. |
| 5 | Navigate to Settings → Credentials and open a credential that referenced the hidden secret | Target page/section loads successfully. |
| 6 | Verify the credential still functions (existing authentication continues to work) | Condition holds as described. |
| 7 | Verify the hidden secret no longer appears in the secret selection dropdown when creating or editing a new credential | Condition holds as described. |

---

## Expected Final State

Verify the hidden secret no longer appears in the secret selection dropdown when creating or editing a new credential.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Hiding a secret used by existing credentials does not break those credentials.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
