---
id: ELITEA-3803
title: "[EliteaAI/elitea_issues#5294] Post-Logout MCP Tool Unavailability — Verify MCP tools return auth error"
priority: high
type: functional
module: mcp-servers
status: ready
execution_type: manual
tags: [issue:5294, r-2.0.5, feat:mcp-remote, eng:backend, eng:frontend, nfr:usability, logout-button, mcp-auth]
requirements: [EliteaAI/elitea_issues#5294]
---

# ELITEA-3803: [EliteaAI/elitea_issues#5294] Post-Logout MCP Tool Unavailability

**Module:** Mcp Servers · **Priority:** High · **Type:** Functional

**Objective:** Verify that after logout, MCP tools cannot be invoked and system returns an authentication error instead of executing the tool.

## Preconditions

- Logged in to ELITEA ({{base_url}})
- A preconfigured Remote MCP is added to Chat conversation with available tools (e.g., "search", "fetch", "execute")
- MCP is currently authenticated
- User knows which MCP tool is available for invocation

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | In Chat with MCP participant, prompt the chat to invoke an MCP tool (e.g., "Use the MCP search tool to find X"). | Chat sends request to MCP; tool invocation is prepared. |
| 2 | Observe the tool invocation succeeds (MCP returns result). Tool execution completes successfully. | Chat displays MCP tool result in response. |
| 3 | Click the Logout button on the MCP toolbar. | Logout succeeds; logout button hidden; login button visible. |
| 4 | Prompt Chat again to invoke the same MCP tool (e.g., "Use the MCP search tool to find Y"). | Chat attempts to invoke MCP tool. |
| 5 | Observe the API response/error returned to Chat. | Request to MCP returns 401 Unauthorized or 403 Forbidden or similar auth error. |
| 6 | Verify Chat displays error message to user indicating authentication failure. | Error message displayed to user: "MCP authentication failed", "Please login to use this tool", or similar. |
| 7 | Confirm MCP tool is NOT executed despite the request. | Tool result is not generated; no side effects from tool execution occur. |

## Expected Final State

- MCP tool invocation is blocked due to missing authentication
- User receives clear error message indicating login is required
- Tool is not executed

## Pass/Fail Criteria

**Pass:** Post-logout tool invocation returns auth error; tool not executed; error message shown.  
**Fail:** Tool executes after logout; no error returned; user is not informed; unexpected tool results appear.
