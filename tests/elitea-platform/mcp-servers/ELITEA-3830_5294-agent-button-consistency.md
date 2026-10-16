---
id: ELITEA-3830
title: "[EliteaAI/elitea_issues#5294] Agent Chat: Button Placement Consistency"
priority: high
type: functional
module: mcp-servers
status: ready
execution_type: manual
tags: [issue:5294, r-2.0.5, feat:mcp-remote, eng:backend, eng:frontend, nfr:usability, logout-button, mcp-auth, agent-config]
requirements: [EliteaAI/elitea_issues#5294]
---

# ELITEA-3830: [EliteaAI/elitea_issues#5294] Agent Chat: Button Placement Consistency

**Module:** Mcp Servers · **Priority:** High · **Type:** Functional

**Objective:** Verify that logout, login, and status buttons are positioned consistently across Chat, Agent-in-Chat, and Agent configuration screens.

## Preconditions

- Logged in to ELITEA ({{base_url}})
- Agent with MCP toolkit is configured and in authenticated state
- Chat conversation with the Agent is available
- All three screens accessible: Chat (direct MCP), Agent-in-Chat, Agent configuration

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat with direct MCP participant. Observe MCP toolbar button layout. | MCP toolbar displays logout, status, and other action buttons in specific positions. Document button order and spacing. |
| 2 | Navigate to Agent-in-Chat interface (invoke Agent with MCP in Chat). Observe MCP toolbar button layout. | Agent-in-Chat displays same MCP toolbar. Verify buttons are in same positions as Chat. |
| 3 | Compare button positioning between Chat and Agent-in-Chat. | Logout button in same relative position; status button in same relative position; spacing consistent. |
| 4 | Navigate to Agent configuration page. Observe MCP toolkit toolbar button layout. | Agent configuration displays MCP toolbar. Verify buttons are in same positions as other screens. |
| 5 | Compare button positioning across all three screens. | Logout, login, and status buttons consistently positioned; alignment matches; spacing uniform. |
| 6 | Verify responsive behavior: resize browser window on each screen. | Buttons maintain consistent relative positioning on different screen sizes; no layout breakage. |

## Expected Final State

- Logout button placed consistently across all three screens
- Login button placed consistently across all three screens
- Status indicator placed consistently
- Button spacing and alignment uniform
- Layout responsive and adaptive

## Pass/Fail Criteria

**Pass:** Buttons consistently positioned and aligned across Chat, Agent-in-Chat, and Agent screens; responsive design works.  
**Fail:** Buttons in different positions on different screens; spacing varies; layout breaks on resize; inconsistent UI.
