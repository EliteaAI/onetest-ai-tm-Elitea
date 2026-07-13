---
id: ELITEA-1970
title: "Credential — Test Connection"
priority: low
type: functional
module: toolkits-credentials
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:toolkits]
requirements: []
---

# ELITEA-1970: Credential — Test Connection

**Module:** toolkits-credentials · **Priority:** low · **Type:** functional

**Objective:** Verify that the "Test connection" button correctly validates credentials against the target service, showing a success toast on a valid token and an inline error indicator on an invalid token.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists and the Credentials section is accessible.
- A valid authentication token for the credential type is available.

---

## Test Data

| Field | Value |
|-------|-------|
| Credential type | Github |
| Valid token | (a working Github personal access token) |
| Invalid token | invalid_token_xyz |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a Github credential with a valid authentication token | Credential is created and saved successfully |
| 2 | Open the credential detail page | Credential detail page loads |
| 3 | Click the "Test connection" button | Success indicator appears with a toast message "The connection is OK!" |
| 4 | Edit the token field to an invalid value (e.g., "invalid_token_xyz") | Token field updates with the invalid value |
| 5 | Click "Test connection" again | Failure/error indicator appears in the token field with a message such as "Invalid token. Please verify the token and try again." |

---

## Expected Final State

The Test connection button provides accurate feedback: a success toast for valid credentials and an inline error message for invalid credentials.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Valid token produces the "The connection is OK!" toast; invalid token shows an inline error in the token field.

**Fail:**
- Any step produces an error or unexpected result.
- Success toast appears for invalid credentials, or error does not appear for an invalid token.
