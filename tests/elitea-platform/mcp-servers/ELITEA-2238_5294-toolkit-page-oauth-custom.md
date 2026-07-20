---
id: ELITEA-2238
title: "[EliteaAI/elitea_issues#5294] Toolkit Page: Login/Logout Auth Flow (OAuth 2.0 & Custom Headers)"
priority: high
type: functional
module: mcp-servers
status: ready
execution_type: manual
tags: [issue:5294, r-2.0.5, feat:mcp-remote, eng:backend, eng:frontend, nfr:usability, logout-button, mcp-auth, toolkit-page]
requirements: [EliteaAI/elitea_issues#5294]
---

# ELITEA-2238: [EliteaAI/elitea_issues#5294] Toolkit Page: Login/Logout Auth Flow (OAuth 2.0 & Custom Headers)

**Module:** Mcp Servers · **Priority:** High · **Type:** Functional

**Objective:** Verify that login and logout flows work correctly on the Toolkit page for both OAuth 2.0 and Custom Headers authentication types.

## Preconditions

- Logged in to ELITEA ({{base_url}})
- User can navigate to Settings → MCPs (Toolkit page)
- Two unauthenticated MCPs available: one with OAuth 2.0, one with Custom Headers auth
- Both MCPs initially show unauthenticated status on Toolkit page

## Test Data

| MCP | Auth Type | Credentials |
|-----|-----------|-------------|
| MCP A | OAuth 2.0 | Valid client_id, client_secret |
| MCP B | Custom Headers | Valid header names and values |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Settings → MCPs (Toolkit page). | Toolkit page loads; MCP A and MCP B visible. |
| 2 | Observe MCP A status: unauthenticated. Click Login button. | OAuth 2.0 authorization flow begins. |
| 3 | Complete OAuth 2.0 flow (provider login, consent). | OAuth flow completes; redirect to Toolkit page. |
| 4 | Verify MCP A status updated to "Authenticated" on Toolkit page. | Status shows authenticated; logout button visible. |
| 5 | Click Logout button on MCP A. | Logout succeeds; status reverts to "Unauthenticated"; login button visible. |
| 6 | Observe MCP B status: unauthenticated. Click Login button. | Custom Headers login flow begins; prompt for header values. |
| 7 | Enter custom header name and value; submit. | Custom headers stored successfully. |
| 8 | Verify MCP B status updated to "Authenticated" on Toolkit page. | Status shows authenticated; logout button visible. |
| 9 | Click Logout button on MCP B. | Logout succeeds; status reverts to "Unauthenticated"; login button visible. |

## Expected Final State

- OAuth 2.0 login/logout flows work on Toolkit page
- Custom Headers login/logout flows work on Toolkit page
- Status updates correctly after each action
- No cross-contamination between MCP A and MCP B

## Pass/Fail Criteria

**Pass:** Both auth types login/logout successfully on Toolkit page; status updates correctly.  
**Fail:** Either auth type fails; status does not update; logout does not clear credentials.
