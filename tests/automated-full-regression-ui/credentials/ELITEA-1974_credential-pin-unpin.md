---
id: ELITEA-1974
title: "Credential — Pin/Unpin"
priority: high
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:toolkits]
requirements: []
---

# ELITEA-1974: Credential — Pin/Unpin

**Module:** toolkits-credentials · **Priority:** medium · **Type:** functional

**Objective:** Verify that a credential can be pinned to the top of the credentials list and unpinned to return it to its normal position.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists with at least one credential.
- The Credentials section is accessible.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Credentials list | Credentials list page loads |
| 2 | Find a credential and click the "Pin to top" button | Credential moves to the top of the list |
| 3 | Navigate to the pinned credential's detail page | Credential detail page loads |
| 4 | Click on the three-dot menu | Dropdown menu opens |
| 5 | Verify the button now shows "Unpin from top" | Menu option displays "Unpin from top" |
| 6 | Click "Unpin from top" | Credential is unpinned |
| 7 | Verify the credential returns to its normal position in the list | Credential is no longer at the top |

---

## Expected Final State

The credential is successfully pinned to the top of the list and then unpinned back to its normal position.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Pinning moves the credential to the top; unpinning returns it to normal position.

**Fail:**
- Any step produces an error or unexpected result.
- Pin/unpin action does not change the credential's position in the list.
