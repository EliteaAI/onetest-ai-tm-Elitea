---
id: ELITEA-1963
title: "Edit Credential — Rename"
priority: high
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:toolkits]
requirements: []
---

# ELITEA-1963: Edit Credential — Rename

**Module:** toolkits-credentials · **Priority:** high · **Type:** functional

**Objective:** Verify that a user can rename an existing credential, that the change persists after a page reload, and that the auto-generated ID field remains unchanged throughout the edit.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists and the Credentials section is accessible.

---

## Test Data

| Field | Value |
|-------|-------|
| Initial Display Name | autotest_cred_edit |
| Credential type | Github |
| Renamed Display Name | autotest_cred_renamed |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a credential "autotest_cred_edit" of type Github | Credential is created successfully |
| 2 | Open the credential detail page | Credential detail page loads with "autotest_cred_edit" displayed |
| 3 | Change Display Name to "autotest_cred_renamed" | Input field updates with the new name |
| 4 | Verify the Save button becomes enabled | Save button is active/clickable |
| 5 | Click Save | Credential is saved with the new name |
| 6 | Reload the page | Page reloads |
| 7 | Verify Display Name shows "autotest_cred_renamed" | Renamed value persisted correctly |
| 8 | Verify the ID field remains unchanged (auto-generated, disabled) | ID field has the original auto-generated value and is not editable |

---

## Expected Final State

The credential is renamed to "autotest_cred_renamed", the change persists after reload, and the auto-generated ID field remains unchanged and read-only.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Display Name is updated to "autotest_cred_renamed" and persists after page reload; ID field remains the same.

**Fail:**
- Any step produces an error or unexpected result.
- The renamed value does not persist after reload, or the ID field changes unexpectedly.
