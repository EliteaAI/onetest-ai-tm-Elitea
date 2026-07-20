---
id: ELITEA-2230
title: "[EliteaAI/elitea_issues#5294] Chat Using Agent with Toolkit: No Cross-Toolkit Impact"
priority: high
type: functional
module: mcp-servers
status: ready
execution_type: manual
tags: [issue:5294, r-2.0.5, feat:mcp-remote, eng:backend, eng:frontend, nfr:usability, logout-button, mcp-auth, agent-in-chat]
requirements: [EliteaAI/elitea_issues#5294]
---

# ELITEA-2230: [EliteaAI/elitea_issues#5294] Chat Using Agent with Toolkit: No Cross-Toolkit Impact

**Module:** Mcp Servers · **Priority:** High · **Type:** Functional

**Objective:** Verify that logging out from one MCP toolkit in an Agent-in-Chat interface does not affect the authentication state of other MCP toolkits in the same Agent.

## Preconditions

- Logged in to ELITEA ({{base_url}})
- An Agent is configured with multiple MCP toolkits (at least 2 MCPs as toolkits)
- Both MCPs are in authenticated state
- Chat conversation open with ability to invoke the Agent

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | In Chat, invoke the Agent. Agent-in-Chat interface opens. | Agent-in-Chat interface displays all configured MCP toolkits. |
| 2 | Observe MCP toolkit #1 toolbar. Verify logout button visible (authenticated). | MCP #1 shows logout button; authenticated state. |
| 3 | Observe MCP toolkit #2 toolbar. Verify logout button visible (authenticated). | MCP #2 shows logout button; authenticated state. |
| 4 | Click Logout button on MCP #1 toolbar. | Logout succeeds for MCP #1; login button now visible for MCP #1. |
| 5 | Verify MCP #2 toolbar remains unchanged: logout button still visible. | MCP #2 remains authenticated; logout button visible. |
| 6 | Attempt to invoke a tool from MCP #2. | MCP #2 tool invocation succeeds (no auth error). |
| 7 | Attempt to invoke a tool from MCP #1. | MCP #1 tool invocation returns auth error (logged out). |

## Expected Final State

- MCP #1 logged out while MCP #2 remains authenticated
- Only MCP #1 tools blocked; MCP #2 tools work normally
- No cross-contamination between toolkit auth states

## Pass/Fail Criteria

**Pass:** Logout in MCP #1 does not affect MCP #2; both auth states independent.  
**Fail:** Logout in MCP #1 also logs out MCP #2; both toolkits affected unexpectedly.
