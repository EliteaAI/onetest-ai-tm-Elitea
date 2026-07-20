---
id: ELITEA-2224
title: "[EliteaAI/elitea_issues#5294] Chat Using Toolkit: Logout Button Visibility"
priority: high
type: functional
module: mcp-servers
status: ready
execution_type: manual
tags: [issue:5294, r-2.0.5, feat:mcp-remote, eng:backend, eng:frontend, nfr:usability, logout-button, mcp-auth, chat-toolkit]
requirements: [EliteaAI/elitea_issues#5294]
---

# ELITEA-2224: [EliteaAI/elitea_issues#5294] Chat Using Toolkit: Logout Button Visibility

**Module:** Mcp Servers · **Priority:** High · **Type:** Functional

**Objective:** Verify that when a preconfigured Remote MCP is added as a participant to a Chat conversation, the logout button is visible and accessible on the MCP toolbar in the Chat interface.

## Preconditions

- Logged in to ELITEA ({{base_url}})
- User can create/edit Chat conversations and add MCP participants
- A preconfigured Remote MCP is available (must support OAuth 2.0 or Custom Headers auth)
- MCP is in authenticated state (user has logged in previously or credential is pre-configured)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create a new Chat conversation or open an existing one. | Chat conversation page opens. |
| 2 | Click "Add Participant" or similar button to add an MCP. | MCP selection panel opens. |
| 3 | Select the preconfigured Remote MCP from the list. | MCP is added to the conversation. |
| 4 | Observe the Chat right panel where participants are listed. | MCP participant appears with toolbar. |
| 5 | In the MCP toolbar, verify the Logout button is present and visible. | Logout button is clearly visible (not hidden, not disabled). |
| 6 | Verify the Logout button is positioned near or adjacent to the MCP name/icon. | Button placement is logical and consistent with UI design. |
| 7 | Hover over or focus the Logout button to verify it is interactive. | Button shows hover state (color change, tooltip, or similar) indicating it is interactive. |

## Expected Final State

- MCP participant added to Chat conversation
- Logout button visible on MCP toolbar in Chat interface
- Button is positioned logically and is interactive
- Button is not disabled or grayed out

## Pass/Fail Criteria

**Pass:** Logout button visible, accessible, and interactive in Chat MCP toolbar.  
**Fail:** Logout button missing, hidden, disabled, or in wrong location.
