---
id: ELITEA-1232
title: "[EliteaAI/elitea_issues#4660] SharePoint — Expired Access Token with Valid Refresh Token Sent to Backend as `access_token: null`"
priority: high
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [feat:credentials, int:sharepoint, feat:toolkits, issue:4660, int:oauth, r-2.0.3]
requirements: [4660]
---
# ELITEA-1232: [EliteaAI/elitea_issues#4660] SharePoint — Expired Access Token with Valid Refresh Token Sent to Backend as `access_token: null`

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify the frontend `getAllTokens()` behavior when the access token is expired but a refresh token exists. The expired token must NOT be excluded — instead it is sent with `access_token: null` and `refresh_token` populated, allowing the backend to use the refresh token proactively before the first API call.

## Preconditions

SharePoint toolkit authenticated
Access token is expired (past `expires_at` timestamp in sessionStorage)
Refresh token is still valid in sessionStorage
Browser DevTools Network tab open

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | With an expired access token and valid refresh token in sessionStorage, send a chat message to an agent that has the SharePoint toolkit. Inspect the outgoing WebSocket or HTTP message payload in Network tab. | The `mcp_tokens` payload sent to the backend contains the SharePoint URL entry with `access_token: null` and `refresh_token: '<valid_token_string>'`. The expired token is NOT omitted entirely. |
| 2 | Observe the agent's response — does it complete the SharePoint tool call without a login prompt? | SharePoint tool call succeeds. Backend received `refresh_token`, performed token exchange with Azure AD, and used the new `access_token` for the API call. No 'Logon' prompt shown. |
| 3 | After the call, inspect sessionStorage `mc_mcp_tokens` entry for SharePoint. | Token entry is updated with a new non-expired `access_token` and updated `expires_at`. The new `refresh_token` (possibly rotated) is also stored. |

## Expected Final State

Token entry is updated with a new non-expired `access_token` and updated `expires_at`. The new `refresh_token` (possibly rotated) is also stored.

## Pass/Fail Criteria

Payload contains `{access_token: null, refresh_token: '...'}` for expired token with refresh token
SharePoint tool call succeeds without user login interaction
SessionStorage updated with new valid access_token after call
