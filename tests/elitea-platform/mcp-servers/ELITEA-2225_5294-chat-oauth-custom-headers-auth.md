---
id: ELITEA-2225
title: "[EliteaAI/elitea_issues#5294] Chat Using Toolkit: Login/Logout Auth Flow (OAuth 2.0 & Custom Headers)"
priority: high
type: functional
module: mcp-servers
status: ready
execution_type: manual
tags: [issue:5294, r-2.0.5, feat:mcp-remote, eng:backend, eng:frontend, nfr:usability, logout-button, mcp-auth, chat-toolkit]
requirements: [EliteaAI/elitea_issues#5294]
---

# ELITEA-2225: [EliteaAI/elitea_issues#5294] Chat Using Toolkit: Login/Logout Auth Flow

**Module:** Mcp Servers · **Priority:** High · **Type:** Functional

**Objective:** Verify that login and logout flows work correctly for MCPs in Chat conversations, supporting both OAuth 2.0 and Custom Headers authentication types.

## Preconditions

- Logged in to ELITEA ({{base_url}})
- Two Chat conversations open (or ability to create them)
- One MCP with OAuth 2.0 auth available; one with Custom Headers auth available
- Both MCPs initially in unauthenticated state

## Test Data

| Auth Type | Login Credentials | Expected Result |
|-----------|-----------------|-----------------|
| OAuth 2.0 | Valid client_id, client_secret | Access token obtained |
| Custom Headers | Valid header names and values | Headers stored and applied |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | In Chat conversation, add OAuth 2.0 MCP as participant. | MCP added; login button visible. |
| 2 | Click Login button; complete OAuth 2.0 authorization flow. | OAuth provider login completed; access token obtained. |
| 3 | Verify MCP toolbar updates: logout button now visible, login button hidden. | Logout button visible; authenticated state shown. |
| 4 | Click Logout button. Verify logout succeeds. | Logout succeeds; UI reverts to showing login button. |
| 5 | Click Login again to re-authenticate. | OAuth 2.0 flow completes again; logout button visible again. |
| 6 | In separate Chat, add Custom Headers MCP as participant. | MCP added; login button visible. |
| 7 | Click Login button; enter custom header values when prompted. | Custom headers stored successfully. |
| 8 | Verify MCP toolbar: logout button visible, login button hidden. | Logout button visible; authenticated state shown. |
| 9 | Click Logout button. Verify logout succeeds. | Logout succeeds; UI reverts to showing login button. |

## Expected Final State

- OAuth 2.0 MCP login/logout cycles complete successfully
- Custom Headers MCP login/logout cycles complete successfully
- UI reflects authentication state changes in both cases
- No errors or unexpected behavior

## Pass/Fail Criteria

**Pass:** Both auth types login/logout successfully; UI updates correctly in Chat.  
**Fail:** Either auth type fails; UI does not update; logout does not clear credentials.
