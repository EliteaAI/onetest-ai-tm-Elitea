---
id: ELITEA-0728
title: "Verify MCP server connection status updates in real-time after state changes"
priority: high
type: functional
module: mcp-servers
status: draft
execution_type: manual
tags: [feat:mcp]
requirements: []
---
# ELITEA-0728: Verify MCP server connection status updates in real-time after state changes

**Module:** Mcp Servers · **Priority:** High · **Type:** Functional

**Objective:** The MCP server connection status indicator does not update when the actual connection state changes. After connecting, disconnecting, or when a server goes down, the displayed status remains stale and does not reflect the current connection state, misleading users about server availability.

## Preconditions

User is logged into Elitea platform
At least one MCP server is configured in the system
User has permission to manage MCP servers
User has access to MCP management page

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the MCP servers page and identify a configured MCP server with a visible connection status indicator | MCP page loads showing the list of configured servers with their current connection status displayed (e.g., Connected, Disconnected, Unknown) |
| 2 | Note the current connection status of the MCP server. If it shows 'Connected', verify the server is actually reachable | Status indicator accurately reflects the current server state |
| 3 | If the server is connected, trigger a disconnect action (e.g., disable the server or use a disconnect button if available) | Connection status updates to 'Disconnected' or equivalent within a reasonable time (< 10 seconds) |
| 4 | Reconnect the MCP server (enable it or click connect) | Connection status updates to 'Connected' or equivalent, reflecting the successful reconnection |
| 5 | Navigate away from the MCP page (e.g., to Chat), wait 30 seconds, then navigate back to MCP page | MCP page shows the current accurate connection status, not a cached/stale status from the previous visit |
| 6 | With the MCP server in a known state, refresh the browser page (F5) | After page reload, connection status correctly reflects the actual server state |
| 7 | Open the MCP server details/configuration and check if the status is consistent with the list view | Detail view shows the same connection status as the list view — no inconsistency between views |
| 8 | If a manual refresh/reconnect button exists, click it and verify the status updates | Manual refresh triggers a real-time status check and updates the indicator accordingly |
| 9 | Rapidly toggle the connection state 3-4 times (connect-disconnect-connect-disconnect) and verify the final status matches the last action taken | Final status accurately reflects the last action (connected or disconnected). No stale intermediate states displayed. Status does not flicker between old and new states |
| 10 | While an MCP server is connected, navigate to an agent that uses this MCP server and verify the MCP connection status is reflected in the agent's toolkit/MCP section | Agent's MCP section shows the server as connected/available. The connection status is consistent between the MCP management page and the agent configuration view |
| 11 | Disconnect the MCP server, then attempt to use it in a chat session (send a message that would trigger MCP tool use) | Chat returns a clear error or fallback message indicating the MCP server is unavailable — no hanging request, no timeout without feedback, and no false success message. The error is actionable (suggests reconnecting) |
| 12 | Reconnect the MCP server and immediately send the same chat message to verify recovery works without requiring a page refresh or session restart | After reconnection, the MCP tool call succeeds on the next attempt without needing to refresh the page or restart the chat session. Recovery is seamless |

## Expected Final State

After reconnection, the MCP tool call succeeds on the next attempt without needing to refresh the page or restart the chat session. Recovery is seamless

## Pass/Fail Criteria

PASS: Status indicator updates within 10 seconds of state changes, remains accurate after page navigation/refresh, is consistent between list/detail/agent views, rapid toggling settles on correct final state, disconnected MCP produces actionable chat error, reconnection recovers seamlessly
FAIL: Status remains stale after connection changes, shows incorrect state after navigation/refresh, is inconsistent between views, rapid toggling shows wrong state, disconnected MCP causes silent failure or hang in chat, or reconnection requires page refresh to take effect
