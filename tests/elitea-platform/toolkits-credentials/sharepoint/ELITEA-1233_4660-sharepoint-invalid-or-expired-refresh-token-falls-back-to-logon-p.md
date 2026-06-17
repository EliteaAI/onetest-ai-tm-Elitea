---
id: ELITEA-1233
title: "[#4660] SharePoint — Invalid or Expired Refresh Token Falls Back to Logon Prompt (McpAuthorizationRequired)"
priority: high
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [feat:credentials, int:sharepoint, error-handling, feat:toolkits, issue:4660, int:oauth, r-2.0.3]
requirements: [4660]
---
# ELITEA-1233: [#4660] SharePoint — Invalid or Expired Refresh Token Falls Back to Logon Prompt (McpAuthorizationRequired)

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify that when the refresh token is invalid or expired, the automatic token refresh attempt fails (`_try_refresh_token()` returns False), a `McpAuthorizationRequired` exception is raised by the backend, and the user sees the SharePoint 'Logon' re-authentication modal — not a generic error or silent failure.

## Preconditions

SharePoint toolkit previously authenticated
Access token is expired
Refresh token is either: (a) manually corrupted in sessionStorage, or (b) revoked in Azure AD portal, or (c) expired (Azure AD refresh token lifetime exceeded)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Corrupt the refresh token in sessionStorage: open DevTools → Application → Session Storage → `mc_mcp_tokens`, edit the SharePoint entry and change `refresh_token` to an invalid string. | SessionStorage updated with invalid refresh token. |
| 2 | Send a chat message to a SharePoint-enabled agent requesting any SharePoint operation. | Backend attempts token refresh with the invalid refresh token → Azure AD rejects it → `_try_refresh_token()` returns False → `McpAuthorizationRequired` exception raised. |
| 3 | Observe the UI response in Chat. | The SharePoint 'Logon' re-authentication modal appears in Chat. The user is prompted to re-authenticate. No generic 'tool execution failed' error is shown. No silent failure occurs. |
| 4 | Click the Logon button in the modal, complete fresh authentication. | OAuth flow completes successfully. New valid access_token and refresh_token stored. Subsequent SharePoint tool calls succeed without interruption. |

## Expected Final State

OAuth flow completes successfully. New valid access_token and refresh_token stored. Subsequent SharePoint tool calls succeed without interruption.

## Pass/Fail Criteria

Invalid refresh token causes McpAuthorizationRequired (not a generic error)
User sees Logon re-authentication modal in Chat
No silent failure — operation does not return empty result without explanation
Re-authentication via Logon modal restores normal operation
