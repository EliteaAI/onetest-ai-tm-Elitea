---
id: ELITEA-2236
title: "[EliteaAI/elitea_issues#5294] Toolkit Page: Status Display on Toolkit Page"
priority: high
type: functional
module: mcp-servers
status: ready
execution_type: manual
tags: [issue:5294, r-2.0.5, feat:mcp-remote, eng:backend, eng:frontend, nfr:usability, logout-button, mcp-auth, toolkit-page]
requirements: [EliteaAI/elitea_issues#5294]
---

# ELITEA-2236: [EliteaAI/elitea_issues#5294] Toolkit Page: Status Display on Toolkit Page

**Module:** Mcp Servers · **Priority:** High · **Type:** Functional

**Objective:** Verify that the MCP authentication status indicator/button is visible and accurate on the Toolkit page, showing whether the MCP is authenticated or unauthenticated.

## Preconditions

- Logged in to ELITEA ({{base_url}})
- User can navigate to Settings → MCPs (Toolkit management page)
- Multiple MCPs configured: some authenticated, some unauthenticated
- Status indicator visible for each MCP

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Settings → MCPs (Toolkit page). | Toolkit page loads; list of MCPs displayed. |
| 2 | Observe the status indicator/button for authenticated MCPs. | Status shows "Authenticated", "Connected", or similar (with visual indicator: green dot, check icon). |
| 3 | Observe the status indicator/button for unauthenticated MCPs. | Status shows "Unauthenticated", "Not Connected", or similar (with visual indicator: gray dot, question mark). |
| 4 | Click on an authenticated MCP to view details. | MCP detail view opens; status shows "Authenticated". |
| 5 | Click Logout button; logout succeeds. | Status updates to "Unauthenticated". |
| 6 | Without page refresh, return to Toolkit page list. | Status in list also shows "Unauthenticated" (real-time update). |
| 7 | Click on an unauthenticated MCP; click Login button. Complete auth flow. | MCP authenticates; status updates to "Authenticated". |
| 8 | Without page refresh, return to Toolkit page list. | Status in list also shows "Authenticated" (real-time update). |

## Expected Final State

- Status indicator accurate for all MCPs on Toolkit page
- Status updates in real-time after login/logout
- No page refresh required for status updates
- Visual indicators clear and consistent

## Pass/Fail Criteria

**Pass:** Status indicator accurate; real-time updates; clear visual indicators for auth state.  
**Fail:** Status indicator missing or inaccurate; requires page refresh; visual indicators unclear.
