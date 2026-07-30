---
id: ELITEA-2227
title: "[EliteaAI/elitea_issues#5294] Chat Using Toolkit: Logout Prevents Tool Invocation"
priority: high
type: functional
module: mcp-servers
status: ready
execution_type: manual
tags: [issue:5294, r-2.0.5, feat:mcp-remote, eng:backend, eng:frontend, nfr:usability, logout-button, mcp-auth, chat-toolkit]
requirements: [EliteaAI/elitea_issues#5294]
---

# ELITEA-2227: [EliteaAI/elitea_issues#5294] Chat Using Toolkit: Logout Prevents Tool Invocation

**Module:** Mcp Servers · **Priority:** High · **Type:** Functional

**Objective:** Verify that after logging out an MCP in Chat, attempting to invoke MCP tools returns an authentication error and the tool is not executed.

## Preconditions

- Logged in to ELITEA ({{base_url}})
- Chat conversation with authenticated MCP participant is open
- MCP has available tools that can be invoked (e.g., "search", "fetch")
- User knows at least one MCP tool name

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | In Chat with authenticated MCP, prompt to invoke an MCP tool (e.g., "Use the MCP search tool to find X"). | Chat invokes MCP tool; tool executes and returns result. |
| 2 | In Chat message history, verify tool result is displayed. | MCP tool result shows in conversation. |
| 3 | Click Logout button on MCP toolbar. | Logout succeeds; login button now visible. |
| 4 | Prompt Chat again to invoke the same MCP tool (e.g., "Use the MCP search tool to find Y"). | Chat attempts to invoke MCP tool. |
| 5 | Observe the response: verify an authentication error is returned (401/403). | Chat receives auth error response from MCP; tool is not executed. |
| 6 | Verify Chat displays error message to user (e.g., "MCP authentication required"). | User sees clear error message indicating login is needed. |
| 7 | Confirm no tool result is shown in Chat history (tool was not executed). | Chat message shows only the error; no tool result displayed. |

## Expected Final State

- MCP tool invocation blocked due to logout
- Authentication error returned to Chat
- Tool not executed
- User informed of auth failure

## Pass/Fail Criteria

**Pass:** Tool invocation returns auth error after logout; tool not executed; error message shown.  
**Fail:** Tool executes after logout; no auth error; user not informed of login requirement.
