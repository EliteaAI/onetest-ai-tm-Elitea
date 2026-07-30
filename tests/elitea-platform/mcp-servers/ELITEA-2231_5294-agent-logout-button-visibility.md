---
id: ELITEA-2231
title: "[EliteaAI/elitea_issues#5294] Agent Chat: Logout Button Visibility"
priority: high
type: functional
module: mcp-servers
status: ready
execution_type: manual
tags: [issue:5294, r-2.0.5, feat:mcp-remote, eng:backend, eng:frontend, nfr:usability, logout-button, mcp-auth, agent-config]
requirements: [EliteaAI/elitea_issues#5294]
---

# ELITEA-2231: [EliteaAI/elitea_issues#5294] Agent Chat: Logout Button Visibility

**Module:** Mcp Servers · **Priority:** High · **Type:** Functional

**Objective:** Verify that when an Agent is configured with a preconfigured Remote MCP as a toolkit, the logout button is visible and accessible on the Agent configuration/execution screen.

## Preconditions

- Logged in to ELITEA ({{base_url}})
- User can create and edit Agents
- A preconfigured Remote MCP is available (supports OAuth 2.0 or Custom Headers)
- Agent is configured with the MCP as a toolkit
- MCP is in authenticated state

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agents section. Select or create an Agent that has an MCP toolkit configured. | Agent configuration page opens; MCP toolkit listed. |
| 2 | In the Agent configuration, locate the MCP toolkit section. | MCP toolkit displayed with configuration options. |
| 3 | Observe the MCP toolbar on the Agent configuration screen. Verify logout button is visible. | Logout button is clearly visible on MCP toolbar (not hidden, not disabled). |
| 4 | Verify the logout button placement is logical and consistent with Chat/Agent-in-Chat layouts. | Button positioning matches previous implementations; easy to access. |
| 5 | Verify the logout button is interactive (not grayed out, shows hover state). | Button responds to mouse hover or focus; appears clickable. |

## Expected Final State

- Agent configuration screen displays MCP toolkit
- Logout button visible on MCP toolbar in Agent configuration
- Button is interactive and consistently positioned
- No blocking errors or warnings

## Pass/Fail Criteria

**Pass:** Logout button visible, accessible, and interactive in Agent configuration MCP toolbar.  
**Fail:** Logout button missing, hidden, disabled, or inconsistently positioned.
