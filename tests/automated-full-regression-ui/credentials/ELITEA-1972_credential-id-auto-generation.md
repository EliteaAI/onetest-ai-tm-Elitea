---
id: ELITEA-1972
title: "Credential — ID Auto-Generation"
priority: medium
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:toolkits]
requirements: []
---

# ELITEA-1972: Credential — ID Auto-Generation

**Module:** toolkits-credentials · **Priority:** medium · **Type:** functional

**Objective:** Verify that a credential's ID field is automatically generated as a slug from the Display Name, is read-only, and that the numeric URL-path ID does not change when the Display Name is updated.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists and the Credentials section is accessible.

---

## Test Data

| Field | Value |
|-------|-------|
| Display Name | My Test Credential |
| Expected slug pattern | my_test_credential (or similar) |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a new credential with Display Name: "My Test Credential" | Credential creation form accepts the name |
| 2 | Save the credential | Credential is saved successfully |
| 3 | Open the credential detail page | Credential detail page loads |
| 4 | Verify the ID field is populated with an auto-generated slug (e.g., "my_test_credential" or similar) | ID field contains the auto-generated slug |
| 5 | Verify the ID field is disabled (not editable) | ID field is read-only and cannot be modified |
| 6 | Verify a numeric ID appears in the credential details page URL path (e.g., "credentials/all/142") | URL contains a numeric segment for the credential |
| 7 | Change the Display Name to a new value | Display Name field updates |
| 8 | Verify the numeric ID in the URL does NOT change | URL numeric ID remains the same after renaming |

---

## Expected Final State

The credential ID is auto-generated from the Display Name, remains read-only, and the numeric URL ID is stable regardless of Display Name changes.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- ID field is auto-generated, disabled, and the numeric URL ID remains unchanged after a Display Name update.

**Fail:**
- Any step produces an error or unexpected result.
- ID field is editable, not populated, or the numeric URL ID changes after renaming.
