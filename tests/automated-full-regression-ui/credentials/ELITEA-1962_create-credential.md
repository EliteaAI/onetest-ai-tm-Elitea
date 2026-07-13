---
id: ELITEA-1962
title: "Create Credential"
priority: high
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:toolkits]
requirements: []
---

# ELITEA-1962: Create Credential

**Module:** toolkits-credentials · **Priority:** high · **Type:** functional

**Objective:** Verify that a user can create a new credential by selecting a type, filling in required fields, and confirming the credential appears in the credentials list with correct metadata.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists and the Credentials section is accessible from the sidebar.

---

## Test Data

| Field | Value |
|-------|-------|
| Display Name | autotest_credential |
| Credential type | Github |
| Auth method | Token |
| Token value | (any valid or placeholder token) |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Credentials section from the sidebar | Credentials list page loads |
| 2 | Click the "+" button in the sidebar header to create a new credential | Credential creation form opens |
| 3 | Select credential type "Github" from available options | Github-specific form fields are displayed |
| 4 | Fill in Display Name: "autotest_credential" | Field accepts and displays the entered name |
| 5 | Select "Token" radio button as the auth method | Token input field becomes available |
| 6 | Fill in a Token value | Token field accepts the input |
| 7 | Click Save | Credential is saved successfully |
| 8 | Verify the credential appears in the list with the correct name and type badge | "autotest_credential" is listed with the Github type badge |

---

## Expected Final State

The newly created credential "autotest_credential" is visible in the credentials list with the correct type badge (Github) and is accessible for further operations.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The credential "autotest_credential" appears in the credentials list with the correct type badge after saving.

**Fail:**
- Any step produces an error or unexpected result.
- The credential is not saved or does not appear in the list after creation.
