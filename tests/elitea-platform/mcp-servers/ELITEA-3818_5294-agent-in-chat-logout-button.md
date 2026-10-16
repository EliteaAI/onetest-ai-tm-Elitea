---
id: ELITEA-3818
title: "[EliteaAI/elitea_issues#5294] Chat Using Agent with Toolkit: Logout Button Visibility"
priority: high
type: functional
module: mcp-servers
status: ready
execution_type: manual
tags: [issue:5294, r-2.0.5, feat:mcp-remote, eng:backend, eng:frontend, nfr:usability, logout-button, mcp-auth, agent-in-chat]
requirements: [EliteaAI/elitea_issues#5294]
---

# ELITEA-3818: [EliteaAI/elitea_issues#5294] Chat Using Agent with Toolkit: Logout Button Visibility

**Module:** Mcp Servers · **Priority:** High · **Type:** Functional

**Objective:** Verify that when an Agent with an MCP toolkit is invoked in a Chat conversation (Agent-in-Chat), the logout button is visible and accessible on the MCP toolbar within the Agent-in-Chat interface.

## Preconditions

- Logged in to ELITEA ({{base_url}})
- An Agent is configured with a preconfigured Remote MCP as a toolkit
- The Agent is in authenticated state for the MCP
- A Chat conversation is open with the ability to invoke Agents
- The Agent can be selected and executed in Chat

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | In Chat conversation, invoke the Agent (e.g., click "+" → select Agent from available agents). | Agent-in-Chat interface opens; Agent toolbar/header visible. |
| 2 | In the Agent-in-Chat interface, locate the MCP toolkit indicator or toolbar. | MCP toolkit displayed within Agent-in-Chat interface. |
| 3 | Observe the MCP toolbar within Agent-in-Chat. Verify Logout button is visible. | Logout button is clearly visible on MCP toolbar in Agent-in-Chat. |
| 4 | Verify the Logout button is positioned consistently with the direct Chat MCP toolbar (issue requirement). | Button placement is logical and matches Chat MCP toolbar layout. |
| 5 | Hover or focus the Logout button to verify it is interactive and not disabled. | Button shows interactive state (hover effect, tooltip, etc.). |

## Expected Final State

- Agent-in-Chat interface displays MCP toolbar
- Logout button visible on MCP toolbar in Agent-in-Chat
- Button is interactive and not disabled
- Button placement consistent with Chat MCP toolbar

## Pass/Fail Criteria

**Pass:** Logout button visible, accessible, and interactive in Agent-in-Chat MCP toolbar.  
**Fail:** Logout button missing, hidden, disabled, or inconsistent with Chat MCP toolbar.
