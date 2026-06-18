---
id: ELITEA-1235
title: "[EliteaAI/elitea_issues#4660] SharePoint OAuth — `offline_access` Always Included in Authorization Request + Both Tokens Stored"
priority: high
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [feat:credentials, int:sharepoint, feat:toolkits, issue:4660, int:oauth, r-2.0.3]
requirements: [4660]
---
# ELITEA-1235: [EliteaAI/elitea_issues#4660] SharePoint OAuth — `offline_access` Always Included in Authorization Request + Both Tokens Stored

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify that the OAuth authorization request for SharePoint always includes the `offline_access` scope (unconditionally, regardless of checkbox state), and that after successful authentication both `access_token` and `refresh_token` are stored in browser sessionStorage (`mc_mcp_tokens`).

## Preconditions

SharePoint toolkit is configured with valid Azure AD app credentials
User is not currently authenticated to SharePoint
Browser DevTools available

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits → SharePoint → credential configuration. Note the state of the 'Auto refresh token' checkbox (leave it unchecked). | SharePoint credential form visible. 'Auto refresh token' checkbox is present and unchecked. |
| 2 | Open browser DevTools → Network tab. Click 'Logon' to start the OAuth flow. | Microsoft Azure AD authorization popup opens. |
| 3 | Inspect the authorization URL in the popup (or the redirect request in Network tab). Check the `scope` query parameter. | `offline_access` is present in the scope parameter (e.g., `scope=offline_access+https://graph.microsoft.com/.default`). This is true even though the checkbox is unchecked. |
| 4 | Now check the 'Auto refresh token' checkbox and click 'Logon' again. | Authorization URL again includes `offline_access` in scope. Behavior is identical to step 3. |
| 5 | Complete the OAuth flow (log in and consent). After redirect, open DevTools → Application → Session Storage → `mc_mcp_tokens`. | Token entry for the SharePoint URL contains both `access_token` (non-null JWT string) and `refresh_token` (non-null string). Both are populated after a single authentication. |
| 6 | Note the `expires_at` and `issued_at` values in the stored token. | Both timestamp fields are present, enabling proactive refresh calculation. |

## Expected Final State

Both timestamp fields are present, enabling proactive refresh calculation.

## Pass/Fail Criteria

`offline_access` present in scope regardless of checkbox state
Both `access_token` and `refresh_token` stored in sessionStorage after auth
`expires_at` and `issued_at` timestamps present in token entry
