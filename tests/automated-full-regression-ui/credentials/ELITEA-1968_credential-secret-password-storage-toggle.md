---
id: ELITEA-1968
title: "Credential — Secret/Password Storage Toggle"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:toolkits]
requirements: []
automation_test_id: tests.ui.toolkits.test_credential_secret_password_toggle.TestCredentialSecretPasswordToggle.test_secret_password_storage_toggle
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1704
---

# ELITEA-1968: Credential — Secret/Password Storage Toggle

**Module:** toolkits-credentials · **Priority:** high · **Type:** functional

**Objective:** Verify that the Secret/Password storage toggle on credential form fields allows users to switch between selecting a saved secret from the Elitea Secret vault and entering a masked plaintext password directly.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists with at least one saved secret in the Elitea Secret vault (e.g., "auth_token").
- The Credentials section is accessible.

---

## Test Data

| Field | Value |
|-------|-------|
| Credential type | Github |
| Auth method | Token |
| Existing secret | auth_token |
| Plaintext token | (any placeholder token value) |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a new Github credential with Token auth selected | Credential form is displayed with Token input field |
| 2 | Verify the Secret/Password toggle is visible next to the token input field | Toggle control is present beside the token field |
| 3 | Click "Secret" on the toggle | Dropdown opens showing "SAVED SECRETS" list from the Elitea Secret vault |
| 4 | Verify "New Project Secret" option is available under a CREATE section | "New Project Secret" option is visible in the dropdown |
| 5 | Select an existing secret from the vault list (e.g., "auth_token") | Selected secret name appears in the token field |
| 6 | Switch to "Password" mode using the toggle | Field changes to a masked plaintext input |
| 7 | Type a token value directly | Value is accepted and displayed as masked (hidden) text |

---

## Expected Final State

The Secret/Password toggle correctly switches between vault-linked secret selection and direct masked plaintext input; both modes store valid token values.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Secret mode shows the vault list and accepts a selected secret; Password mode accepts direct masked input.

**Fail:**
- Any step produces an error or unexpected result.
- The toggle does not switch modes, the vault list does not appear, or the selected secret is not displayed.
