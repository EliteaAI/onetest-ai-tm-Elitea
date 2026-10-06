---
id: ELITEA-1932
title: "Edit Remote MCP — Client Secret with Secret/Password Toggle"
priority: critical
type: functional
module: elitea-platform
status: draft
execution_type: manual
tags: [automated:UI:regression]
requirements: []
---

# ELITEA-1932: Edit Remote MCP — Client Secret with Secret/Password Toggle

**Module:** elitea-platform · **Priority:** medium · **Type:** functional

**Objective:** Verify that the Client Secret field supports both "Secret" and "Password" input modes via a toggle, and that the selected mode and its value are persisted after saving.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing Remote MCP is available and open on its detail page in Form view.
- Access to the Elitea secret vault is available.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a Remote MCP detail page in Form view | Detail page loads in Form view |
| 2 | Locate "Client Secret" field | Client Secret field is visible |
| 3 | Verify "secret view toggler" group is visible with "Secret" and "Password" buttons | Toggle group with both buttons is displayed |
| 4 | Verify "Password" button is pressed (active) by default — field shows masked text | Password mode is active and text is masked |
| 5 | Click "Secret" button | Toggle switches to Secret mode |
| 6 | Verify toggle switches to Secret mode | Secret button is now active |
| 7 | Enter a credential reference in Secret mode from Elitea secret vault | Secret reference is entered in the field |
| 8 | Click Save | Operation completes successfully |
| 9 | Reload — verify Client Secret value persisted in chosen mode | Client Secret is shown in Secret mode with the saved reference |

---

## Expected Final State

The Client Secret field retains the entered value in Secret mode after saving and page reload.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Toggle switches between modes; Secret mode value is persisted after save.

**Fail:**
- Any step produces an error or unexpected result.
- Toggle does not function or saved value is lost after reload.
