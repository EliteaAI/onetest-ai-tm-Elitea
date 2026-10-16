---
id: ELITEA-3832
title: "[EliteaAI/elitea_issues#5294] Toolkit Page: Logout from Toolkit Section"
priority: high
type: functional
module: mcp-servers
status: ready
execution_type: manual
tags: [issue:5294, r-2.0.5, feat:mcp-remote, eng:backend, eng:frontend, nfr:usability, logout-button, mcp-auth, toolkit-page]
requirements: [EliteaAI/elitea_issues#5294]
---

# ELITEA-3832: [EliteaAI/elitea_issues#5294] Toolkit Page: Logout from Toolkit Section

**Module:** Mcp Servers · **Priority:** High · **Type:** Functional

**Objective:** Verify that when a preconfigured Remote MCP is viewed in the MCPs/Toolkits section of Settings, the logout button is visible and allows users to logout directly from that page (issue requirement: "Logout button directly on toolkit, no need to navigate back").

## Preconditions

- Logged in to ELITEA ({{base_url}})
- User has permissions to view and manage MCPs in Settings/Toolkits section
- A preconfigured Remote MCP is configured and authenticated
- Navigation to Settings → MCPs (or equivalent Toolkit management page) is available

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Settings → MCPs (or Settings → Toolkits). | MCPs/Toolkits management page loads. |
| 2 | Locate the authenticated preconfigured Remote MCP in the list. | MCP displayed in list; shows authentication status. |
| 3 | Click on the MCP to view its details or configuration. | MCP detail/configuration panel opens. |
| 4 | In the MCP detail view, observe the logout button. | Logout button is visible and accessible (not hidden, not disabled). |
| 5 | Click the Logout button. | Logout API call sent; logout succeeds (200 OK response). |
| 6 | Verify the UI updates: logout button hidden; login button visible. | MCP shows unauthenticated state on Toolkit page. |
| 7 | Navigate to Chat with the same MCP as participant. Verify logout persisted. | Chat MCP shows login button (unauthenticated); logout was global. |

## Expected Final State

- Logout button visible on Toolkit page for authenticated MCPs
- Logout from Toolkit page logs out globally (Chat, Agent, Toolkit all affected)
- MCP status updates immediately on Toolkit page
- UI reflects unauthenticated state

## Pass/Fail Criteria

**Pass:** Logout button visible on Toolkit page; logout succeeds; state updates globally.  
**Fail:** Logout button missing from Toolkit page; logout fails; state changes only locally.
