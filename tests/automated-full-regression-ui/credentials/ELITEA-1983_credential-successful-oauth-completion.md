---
id: ELITEA-1983
title: "Credential — Successful OAuth Completion"
priority: high
type: functional
module: toolkits-credentials
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:toolkits]
requirements: []
---

# ELITEA-1983: Credential — Successful OAuth Completion

**Module:** toolkits-credentials · **Priority:** high · **Type:** functional

**Objective:** Verify that completing OAuth authorization with valid credentials redirects back to the Elitea application, shows a success indicator, changes the Login button to Logout, and allows a successful Test connection using the OAuth token.

---

## Preconditions

- User is logged in to the Elitea platform.
- A SharePoint credential with Delegated auth type and valid OAuth configuration exists.
- Valid OAuth provider credentials are available for completing the login flow.

---

## Test Data

| Field | Value |
|-------|-------|
| Credential type | SharePoint |
| Auth method | Delegated |
| OAuth provider credentials | (valid Microsoft or configured OAuth provider account) |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a SharePoint Delegated credential with valid OAuth configuration | Credential detail page loads |
| 2 | Click the "Login" button | "Configuration OAuth" dialog opens |
| 3 | Verify scopes are pre-populated correctly from the credential's Scopes field | Scope field is pre-filled |
| 4 | Click "Authorize" | Browser redirects to the Microsoft OAuth login page (or configured provider) |
| 5 | Complete OAuth login with valid credentials on the provider page | OAuth provider grants authorization |
| 6 | Verify redirect back to the Elitea application after successful authorization | User is returned to the Elitea credential page |
| 7 | Verify a success indicator or toast message confirming OAuth token was obtained | Success toast or indicator is displayed |
| 8 | Verify the "Login" button changes to "Logout" | Button label is now "Logout" |
| 9 | Click "Test connection" | Connection test succeeds using the OAuth token |

---

## Expected Final State

After successful OAuth authorization, the credential shows a Logout button and a successful Test connection result, confirming the OAuth token is stored and active.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- OAuth flow completes successfully; Login changes to Logout; Test connection succeeds with the OAuth token.

**Fail:**
- Any step produces an error or unexpected result.
- Authorization fails, redirect does not occur, Login button does not change, or Test connection fails after OAuth completion.
