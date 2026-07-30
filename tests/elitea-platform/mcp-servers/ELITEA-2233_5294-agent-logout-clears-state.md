---
id: ELITEA-2233
title: "[EliteaAI/elitea_issues#5294] Agent Chat: Logout Clears Session State"
priority: high
type: functional
module: mcp-servers
status: ready
execution_type: manual
tags: [issue:5294, r-2.0.5, feat:mcp-remote, eng:backend, eng:frontend, nfr:usability, logout-button, mcp-auth, agent-config]
requirements: [EliteaAI/elitea_issues#5294]
---

# ELITEA-2233: [EliteaAI/elitea_issues#5294] Agent Chat: Logout Clears Session State

**Module:** Mcp Servers · **Priority:** High · **Type:** Functional

**Objective:** Verify that when logout is clicked on an MCP in Agent configuration, all authentication tokens, refresh tokens, and cached credentials are cleared from the backend and frontend storage.

## Preconditions

- Logged in to ELITEA ({{base_url}})
- Agent with authenticated MCP toolkit is configured
- Browser DevTools (F12) open with Storage tab available
- MCP currently in authenticated state

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Agent configuration page with authenticated MCP. | Agent configuration loads; MCP shows logout button (authenticated). |
| 2 | Open Browser DevTools → Storage → Local Storage / Session Storage. | Storage inspector open. |
| 3 | Note any stored MCP tokens or credentials (search for "token", "auth", "mcp"). | MCP authentication data visible in storage (e.g., access_token, session_id). |
| 4 | Click Logout button on MCP toolbar. | Logout API call sent to backend. |
| 5 | Verify API response: backend returns success (200 OK). | Response indicates logout success. |
| 6 | In Storage tab, verify all MCP tokens/credentials are removed (refresh storage view). | MCP authentication data removed from local/session storage. |
| 7 | Verify UI updates: logout button hidden; login button visible. | UI reflects unauthenticated state. |
| 8 | Refresh the page (F5). | Page reloads; Agent configuration reloads. |
| 9 | Verify MCP still shows unauthenticated state after page refresh (logout persisted). | Login button visible; MCP remains unauthenticated. |

## Expected Final State

- All MCP tokens and credentials cleared from storage
- UI reflects unauthenticated state
- Logout state persists across page refresh
- Backend session tokens cleared

## Pass/Fail Criteria

**Pass:** Logout clears tokens; UI updates; state persists after page refresh.  
**Fail:** Tokens remain in storage; UI does not update; state reverts after refresh; logout does not persist.
