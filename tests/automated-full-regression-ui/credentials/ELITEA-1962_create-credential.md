---
id: ELITEA-1962
title: "Credential CRUD Journey"
priority: critical
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:toolkits]
requirements: []
---

# ELITEA-1962: Credential CRUD Journey

**Module:** toolkits-credentials · **Priority:** critical · **Type:** functional

**Objective:** Verify the complete credential lifecycle: creation, display in list, rename with persistence, and permanent deletion.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists and the Credentials section is accessible from the sidebar.

---

## Test Data

| Field | Value |
|-------|-------|
| Initial Display Name | autotest_crud_credential |
| Renamed Display Name | autotest_crud_renamed |
| Credential type | Github |
| Auth method | Token |
| Token value | (any valid or placeholder token) |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| **CREATE Phase** | | |
| 1 | Navigate to the Credentials section from the sidebar | Credentials list page loads |
| 2 | Click the "+" button in the sidebar header to create a new credential | Credential creation form opens |
| 3 | Select credential type "Github" from available options | Github-specific form fields are displayed |
| 4 | Fill in Display Name: "autotest_crud_credential" | Field accepts and displays the entered name |
| 5 | Select "Token" radio button as the auth method | Token input field becomes available |
| 6 | Fill in a Token value | Token field accepts the input |
| 7 | Click Save | Credential is saved successfully |
| 8 | Verify the credential appears in the list with the correct name and type badge | "autotest_crud_credential" is listed with the Github type badge |
| **RENAME Phase** | | |
| 9 | Open the credential detail page for "autotest_crud_credential" | Credential detail page loads with the original Display Name |
| 10 | Change Display Name to "autotest_crud_renamed" | Input field updates with the new name |
| 11 | Verify the Save button becomes enabled | Save button is active/clickable |
| 12 | Click Save | Credential is saved with the new name |
| 13 | Reload the page | Page reloads |
| 14 | Verify Display Name shows "autotest_crud_renamed" | Renamed value persisted correctly |
| 15 | Verify the ID field remains unchanged (auto-generated, disabled) | ID field has the original auto-generated value and is not editable |
| **DELETE Phase** | | |
| 16 | Click the three-dot menu and select "Delete" | Delete confirmation dialog appears |
| 17 | Confirm deletion in the dialog | Credential is deleted |
| 18 | Verify the credential is removed from the list | "autotest_crud_renamed" no longer appears in the list |
| 19 | Reload the page and verify the credential is still gone | Credential remains absent after reload |

---

## Expected Final State

The credential lifecycle is complete: created → renamed with persistence → permanently deleted.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Credential is created and appears in the list; rename persists after reload; ID remains unchanged; credential is permanently removed after deletion.

**Fail:**
- Any step produces an error or unexpected result.
- Credential is not saved, rename does not persist, ID changes unexpectedly, or credential reappears after deletion.

---

## Notes

**Source functional tests:** ELITEA-1962 (Create), ELITEA-1963 (Edit/Rename), ELITEA-1964 (Delete)

**Regression rationale:** Consolidates the critical CRUD path into one coherent journey, preserving all essential checkpoints: credential creation, list display, rename persistence, ID stability, and permanent deletion.

**Selected checkpoints:** Credential appears in list with correct badge; rename persists after reload; auto-generated ID remains unchanged; credential is permanently removed and does not reappear.
