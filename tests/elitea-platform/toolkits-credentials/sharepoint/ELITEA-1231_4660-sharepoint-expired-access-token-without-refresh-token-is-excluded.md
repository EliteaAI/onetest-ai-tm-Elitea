---
id: ELITEA-1231
title: "[#4660] SharePoint — Expired Access Token Without Refresh Token Is Excluded; Logon Prompt Shown"
priority: medium
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [feat:credentials, int:sharepoint, error-handling, feat:toolkits, issue:4660, int:oauth, r-2.0.3]
requirements: [4660]
---
# ELITEA-1231: [#4660] SharePoint — Expired Access Token Without Refresh Token Is Excluded; Logon Prompt Shown

**Module:** Sharepoint · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the edge case where the access token is expired AND no refresh token exists in sessionStorage. In this case `getAllTokens()` must exclude the token entry entirely (neither sending an expired access token nor expecting a refresh). The backend receives no SharePoint token and the user is prompted to re-authenticate via the Logon modal.

## Preconditions

SharePoint toolkit previously authenticated
Manually edit sessionStorage `mc_mcp_tokens`: set `access_token` to an expired JWT and remove/delete the `refresh_token` field
Browser DevTools available

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open DevTools → Application → Session Storage → `mc_mcp_tokens`. Edit the SharePoint token entry: set `access_token` to an expired value and delete the `refresh_token` field entirely. | SessionStorage entry now has an expired access_token and no refresh_token. |
| 2 | Send a chat message to a SharePoint-enabled agent. Inspect the outgoing message payload in Network tab. | The `mcp_tokens` payload does NOT contain any entry for the SharePoint URL. The expired-no-refresh token was excluded entirely by `getAllTokens()`. |
| 3 | Observe the UI response. | The SharePoint Logon re-authentication modal appears. No generic error. No silent empty response. |
| 4 | Re-authenticate via the Logon modal. Repeat the tool call. | New access_token and refresh_token stored. SharePoint tool call succeeds. |

## Expected Final State

New access_token and refresh_token stored. SharePoint tool call succeeds.

## Pass/Fail Criteria

No SharePoint token entry in the message payload when access_token expired AND no refresh_token
User sees Logon re-authentication modal
No silent failure or empty tool result returned
After re-authentication, tool call succeeds
