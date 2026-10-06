---
id: ELITEA-1969
title: "Credential — Create New Project Secret from Secret Toggle"
priority: high
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:toolkits]
requirements: []
---

# ELITEA-1969: Credential — Create New Project Secret from Secret Toggle

**Module:** toolkits-credentials · **Priority:** high · **Type:** functional

**Objective:** Verify that a user can navigate from the Secret toggle in the credential form to the Secrets settings page, create a new project secret, and then return to the credential form to see the new secret in the saved secrets list after refreshing.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists and the Credentials section is accessible.

---

## Test Data

| Field | Value |
|-------|-------|
| Credential type | Github |
| Auth method | Token |
| New secret name | autotest_new_secret |
| New secret value | test_value_123 |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a new Github credential with Token auth selected | Credential form is displayed with Token input field |
| 2 | Click "Secret" toggle next to the token field | Dropdown opens showing CREATE section and SAVED SECRETS list |
| 3 | Verify dropdown shows CREATE section with "New Project Secret" option and SAVED SECRETS list | Both sections are present in the dropdown |
| 4 | Click "New Project Secret" | Navigation to the secrets settings page (/settings/secrets) occurs |
| 5 | Verify the Secrets page shows a table with columns: Name, Value, Actions | Secrets table is displayed with the correct columns |
| 6 | Click the "+" button to add a new secret | New secret input row or dialog appears |
| 7 | Fill in Name: "autotest_new_secret" and Value: "test_value_123" | Fields accept the input |
| 8 | Click the checkmark (confirm) to save the secret | New secret is saved |
| 9 | Verify "autotest_new_secret" appears in the secrets table | Secret is listed in the table |
| 10 | Navigate back to the credential creation form | Credential form is displayed |
| 11 | Click "Secret" toggle again on the token field | Dropdown reopens with saved secrets list |
| 12 | Click the refresh button next to "SAVED SECRETS" header | List refreshes |
| 13 | Verify "autotest_new_secret" now appears in the saved secrets list | Newly created secret is visible in the dropdown |

---

## Expected Final State

The new project secret "autotest_new_secret" is created via the secrets settings page and appears in the credential form's saved secrets dropdown after refreshing.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- "autotest_new_secret" is created successfully and appears in the saved secrets dropdown after refresh.

**Fail:**
- Any step produces an error or unexpected result.
- Navigation to the secrets page fails, the secret is not saved, or it does not appear in the dropdown after refresh.
