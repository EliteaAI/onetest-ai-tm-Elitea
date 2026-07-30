---
id: ELITEA-2226
title: "[EliteaAI/elitea_issues#5294] Chat Using Toolkit: Chat to Agent State Independence"
priority: high
type: functional
module: mcp-servers
status: ready
execution_type: manual
tags: [issue:5294, r-2.0.5, feat:mcp-remote, eng:backend, eng:frontend, nfr:usability, logout-button, mcp-auth, chat-toolkit]
requirements: [EliteaAI/elitea_issues#5294]
---

# ELITEA-2226: [EliteaAI/elitea_issues#5294] Chat Using Toolkit: Chat to Agent State Independence

**Module:** Mcp Servers · **Priority:** High · **Type:** Functional

**Objective:** Verify that logging out from an MCP in a Chat conversation does not affect the authentication state of the same MCP when used in an Agent toolkit.

## Preconditions

- Logged in to ELITEA ({{base_url}})
- A Chat conversation has an MCP as a direct participant (authenticated)
- The same MCP is configured as a toolkit in an Agent (authenticated)
- Both are currently in authenticated state

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | In Chat, observe MCP toolbar. Verify logout button is visible (authenticated). | MCP in Chat is authenticated; logout button visible. |
| 2 | In separate Agent configuration page, observe the same MCP toolkit. Verify logout button is visible (authenticated). | MCP in Agent is authenticated; logout button visible. |
| 3 | Return to Chat; click Logout button on the MCP toolbar. | Logout succeeds; Chat MCP now shows login button. |
| 4 | Return to Agent configuration page. Observe MCP toolkit status. | MCP in Agent still shows logout button (remains authenticated). |
| 5 | Verify that MCP tools in Agent can still be invoked without re-authentication. | Agent can invoke MCP tools without errors; authentication persists in Agent. |
| 6 | In Chat, attempt to invoke an MCP tool (now logged out). | MCP tool invocation returns auth error (as expected; Chat MCP is logged out). |

## Expected Final State

- MCP logged out in Chat does not affect MCP auth state in Agent
- MCP remains authenticated in Agent and can invoke tools
- Chat MCP shows auth error when attempting tool invocation

## Pass/Fail Criteria

**Pass:** Logout in Chat does not affect Agent MCP state; Agent tools work while Chat tools fail.  
**Fail:** Logout in Chat also logs out Agent MCP; both fail; auth states linked unexpectedly.
