---
id: ELITEA-2219
title: "[EliteaAI/elitea_issues#5294] Core Logout Functionality — Verify logout clears MCP auth tokens"
priority: high
type: functional
module: mcp-servers
status: ready
execution_type: manual
tags: [issue:5294, r-2.0.5, feat:mcp-remote, eng:backend, eng:frontend, nfr:usability, logout-button, mcp-auth]
requirements: [EliteaAI/elitea_issues#5294]
---

# ELITEA-2219: [EliteaAI/elitea_issues#5294] Core Logout Functionality

**Module:** Mcp Servers · **Priority:** High · **Type:** Functional

**Objective:** Verify that when a user clicks the logout button for a preconfigured remote MCP, authentication tokens and session state are cleared from the backend.

## Preconditions

- Logged in to ELITEA ({{base_url}})
- User has permissions to add/remove MCPs from Chat, Agents, or Toolkit
- A preconfigured Remote MCP is added to a Chat conversation, Agent, or Toolkit page
- MCP is currently in authenticated state (login button is hidden, logout button is visible)
- Browser developer tools (F12) open with Network tab active to monitor API calls

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat/Agent/Toolkit page with authenticated MCP toolkit visible. | Page loads with MCP toolkit displayed and status shows "Authenticated". |
| 2 | Locate the Logout button on the MCP toolkit interface. | Logout button is visible and clickable (not disabled). |
| 3 | Click the Logout button. | API call is made to backend MCP authorization endpoint (observe POST /api/mcp/logout or similar). |
| 4 | Observe the API response in Network tab; verify it returns 200 OK. | Response status is 200; response body contains {"status": "success", "message": "logged out"} or similar. |
| 5 | Check browser local/session storage: confirm MCP tokens are removed (use Storage tab in DevTools). | Tokens for the MCP (access_token, refresh_token, session_id) are no longer present. |
| 6 | Verify UI updates: logout button is hidden and login button becomes visible. | Logout button disappears; Login button appears in its place. |
| 7 | Check MCP status indicator (if present) updates to show "Unauthenticated" or similar state. | Status indicator reflects logout state accurately. |

## Expected Final State

- Backend MCP session tokens are cleared
- User interface reflects unauthenticated state
- Login button visible, logout button hidden
- Status indicator shows "Unauthenticated"

## Pass/Fail Criteria

**Pass:** Logout button triggers successful backend call; tokens removed; UI reflects unauthenticated state; status indicator updated.  
**Fail:** Logout fails with error; tokens still present after logout; UI does not update; logout button remains visible after click.
