---
id: ELITEA-3826
title: "[EliteaAI/elitea_issues#5294] Agent Chat: Login/Logout Auth Flow (OAuth 2.0 & Custom Headers)"
priority: high
type: functional
module: mcp-servers
status: ready
execution_type: manual
tags: [issue:5294, r-2.0.5, feat:mcp-remote, eng:backend, eng:frontend, nfr:usability, logout-button, mcp-auth, agent-config]
requirements: [EliteaAI/elitea_issues#5294]
---

# ELITEA-3826: [EliteaAI/elitea_issues#5294] Agent Chat: Login/Logout Auth Flow

**Module:** Mcp Servers · **Priority:** High · **Type:** Functional

**Objective:** Verify that login and logout flows work correctly for MCPs in Agent configuration screens, supporting OAuth 2.0 and Custom Headers authentication types.

## Preconditions

- Logged in to ELITEA ({{base_url}})
- Two Agents created: Agent A with OAuth 2.0 MCP toolkit, Agent B with Custom Headers MCP toolkit
- Both MCPs initially in unauthenticated state

## Test Data

| Agent | Auth Type | Credentials |
|-------|-----------|-------------|
| Agent A | OAuth 2.0 | Valid client_id, client_secret |
| Agent B | Custom Headers | Valid header names and values |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agent A configuration page. | Agent A configuration loads; MCP toolkit visible. |
| 2 | Observe MCP toolbar. Verify login button visible (unauthenticated). | Login button visible; logout button hidden. |
| 3 | Click Login button. Complete OAuth 2.0 authorization flow. | OAuth 2.0 flow succeeds; access token obtained. |
| 4 | Verify MCP toolbar updates: logout button now visible. | Logout button visible; authenticated state shown. |
| 5 | Click Logout button on MCP toolbar. | Logout succeeds; login button visible again. |
| 6 | Navigate to Agent B configuration page. | Agent B configuration loads; MCP toolkit visible. |
| 7 | Observe MCP toolbar. Verify login button visible (unauthenticated). | Login button visible; logout button hidden. |
| 8 | Click Login button; enter custom header values when prompted. | Custom headers stored successfully. |
| 9 | Verify MCP toolbar: logout button now visible. | Logout button visible; authenticated state shown. |
| 10 | Click Logout button on MCP toolbar. | Logout succeeds; login button visible again. |

## Expected Final State

- OAuth 2.0 and Custom Headers auth flows work on Agent configuration screens
- UI updates reflect authentication state changes
- Login/logout cycles complete successfully
- No errors between Agent A and Agent B operations

## Pass/Fail Criteria

**Pass:** Both auth types login/logout successfully on Agent screens; UI updates correctly.  
**Fail:** Either auth type fails; UI does not update; logout does not clear credentials.
