---
id: ELITEA-1984
title: "Credential — Failed OAuth Completion"
priority: high
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:toolkits]
requirements: []
---

# ELITEA-1984: Credential — Failed OAuth Completion

**Module:** toolkits-credentials · **Priority:** high · **Type:** functional

**Objective:** Verify that the Elitea application handles a failed or cancelled OAuth authorization gracefully, showing an appropriate error or informational message without crashing.

---

## Preconditions

- User is logged in to the Elitea platform.
- A SharePoint credential with Delegated auth type exists.

---

## Test Data

| Field | Value |
|-------|-------|
| Credential type | SharePoint |
| Auth method | Delegated |
| Invalid scope | Invalid.Scope.xyz |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a SharePoint credential with Delegated auth | Credential detail page loads |
| 2 | Click the "Login" button | "Configuration OAuth" dialog opens |
| 3 | Modify scopes to include an invalid scope (e.g., "Invalid.Scope.xyz") | Scope field is updated with the invalid scope |
| 4 | Click "Authorize" | Browser redirects to the OAuth provider login page |
| 5 | Verify the OAuth provider shows an error or denies authorization | Provider displays an error or access denied message |
| 6 | Verify Elitea handles the failure gracefully (shows error message, does not crash) | Elitea displays an informative error message without crashing |
| 7 | Alternatively, click "Authorize" then cancel/close the OAuth provider login page | OAuth provider page is closed by the user |
| 8 | Verify Elitea shows an appropriate message about incomplete or cancelled authorization | Message about incomplete/cancelled authorization is displayed |

---

## Expected Final State

Elitea handles both failed (invalid scope) and cancelled OAuth flows gracefully, displaying appropriate messages without application crashes.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without crashes.
- Failed and cancelled OAuth flows result in clear, user-friendly error/informational messages.

**Fail:**
- Any step causes an application crash or unhandled error.
- Failed or cancelled OAuth flow produces no feedback or a raw error/stack trace.
