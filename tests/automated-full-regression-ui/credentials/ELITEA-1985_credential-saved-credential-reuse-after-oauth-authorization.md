---
id: ELITEA-1985
title: "Credential — Saved Credential Reuse After OAuth Authorization"
priority: medium
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:toolkits]
requirements: []
---

# ELITEA-1985: Credential — Saved Credential Reuse After OAuth Authorization

**Module:** toolkits-credentials · **Priority:** medium · **Type:** functional

**Objective:** Verify that an OAuth-authorized SharePoint credential retains its token after navigation, can be linked to a toolkit, enables toolkit operations, and does not require re-authorization when reused in different contexts.

---

## Preconditions

- User is logged in to the Elitea platform.
- A SharePoint credential with Delegated auth type has been successfully authorized via OAuth ("Logout" button is present).
- A SharePoint toolkit is available or can be created.

---

## Test Data

| Field | Value |
|-------|-------|
| Credential type | SharePoint |
| Auth method | Delegated |
| Required state | OAuth authorization already completed (Logout button present) |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a SharePoint Delegated credential and complete OAuth authorization successfully | Credential shows "Logout" button indicating active OAuth token |
| 2 | Navigate away from the credential (e.g., go to Toolkits or Credentials list) | Navigation occurs successfully |
| 3 | Return to the same credential detail page | Credential page loads |
| 4 | Verify the OAuth token is still valid ("Logout" button is present) | Logout button is still displayed, indicating the token persists |
| 5 | Link this credential to a SharePoint toolkit | Credential is selected in the toolkit configuration |
| 6 | Verify toolkit operations work using the saved OAuth-authorized credential | Toolkit operation completes successfully |
| 7 | Verify no re-authorization prompt appears when reusing the credential in different contexts | No OAuth login prompt is triggered during reuse |

---

## Expected Final State

The OAuth-authorized credential persists its token across navigation, enables toolkit operations, and does not require re-authorization when reused.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- OAuth token persists after navigation; toolkit operations succeed; no re-authorization prompt is shown.

**Fail:**
- Any step produces an error or unexpected result.
- Token is lost after navigation, toolkit operations fail, or re-authorization is required unexpectedly.
