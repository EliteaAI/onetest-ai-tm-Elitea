---
id: ELITEA-1964
title: "Delete Credential"
priority: high
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:toolkits]
requirements: []
---

# ELITEA-1964: Delete Credential

**Module:** toolkits-credentials · **Priority:** high · **Type:** functional

**Objective:** Verify that a user can delete a credential via the three-dot menu, confirm the deletion through the confirmation dialog, and that the credential is permanently removed from the list.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists and the Credentials section is accessible.

---

## Test Data

| Field | Value |
|-------|-------|
| Display Name | autotest_cred_delete |
| Credential type | (any, e.g. Github) |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a credential "autotest_cred_delete" | Credential is created and visible in the list |
| 2 | Verify it appears in the credentials list | "autotest_cred_delete" is listed |
| 3 | Open the credential detail page | Credential detail page loads |
| 4 | Click the three-dot menu and select "Delete" | Delete confirmation dialog appears |
| 5 | Confirm deletion in the dialog | Credential is deleted |
| 6 | Verify the credential is removed from the list | "autotest_cred_delete" no longer appears in the list |
| 7 | Reload the page and verify the credential is still gone | Credential remains absent after reload |

---

## Expected Final State

The credential "autotest_cred_delete" is permanently removed from the credentials list and does not reappear after a page reload.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The credential is removed from the list and stays absent after a page reload.

**Fail:**
- Any step produces an error or unexpected result.
- The credential still appears in the list after deletion or reappears after reload.
