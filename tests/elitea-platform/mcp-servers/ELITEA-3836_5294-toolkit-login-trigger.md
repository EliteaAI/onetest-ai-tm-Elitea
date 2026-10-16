---
id: ELITEA-3836
title: "[EliteaAI/elitea_issues#5294] Toolkit Page: Login Trigger from Toolkit Page"
priority: high
type: functional
module: mcp-servers
status: ready
execution_type: manual
tags: [issue:5294, r-2.0.5, feat:mcp-remote, eng:backend, eng:frontend, nfr:usability, logout-button, mcp-auth, toolkit-page]
requirements: [EliteaAI/elitea_issues#5294]
---

# ELITEA-3836: [EliteaAI/elitea_issues#5294] Toolkit Page: Login Trigger from Toolkit Page

**Module:** Mcp Servers · **Priority:** High · **Type:** Functional

**Objective:** Verify that the login button is visible on unauthenticated MCPs on the Toolkit page, and clicking it initiates the authentication flow.

## Preconditions

- Logged in to ELITEA ({{base_url}})
- User can navigate to Settings → MCPs (Toolkit page)
- An unauthenticated preconfigured Remote MCP is available
- MCP supports OAuth 2.0 or Custom Headers auth

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Settings → MCPs (Toolkit page). | Toolkit page loads; MCP list displayed. |
| 2 | Locate an unauthenticated MCP in the list. | MCP shows status indicating unauthenticated state. |
| 3 | In the MCP list or detail view, locate the Login button. | Login button is visible and accessible (not hidden, not disabled). |
| 4 | Click the Login button. | Login flow initiated; authentication dialog or redirect occurs. |
| 5 | (OAuth 2.0) Complete OAuth 2.0 authorization flow. | OAuth provider login completed; redirect back to Toolkit page with access token. |
| 6 | Alternatively, (Custom Headers) Enter custom header values when prompted. | Custom headers entered and stored successfully. |
| 7 | Verify MCP status updates to "Authenticated" on Toolkit page. | Status indicator changes to "Authenticated"; logout button now visible. |

## Expected Final State

- Login button visible on unauthenticated MCPs on Toolkit page
- Login flow initiates and completes successfully
- Status updates to authenticated after login
- User remains on Toolkit page (no unwanted navigation)

## Pass/Fail Criteria

**Pass:** Login button visible; login flow works; status updates to authenticated; user stays on Toolkit page.  
**Fail:** Login button missing; login flow fails; status does not update; page navigates away unexpectedly.
