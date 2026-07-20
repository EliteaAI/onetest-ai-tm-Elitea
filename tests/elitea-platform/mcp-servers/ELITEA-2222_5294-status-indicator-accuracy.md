---
id: ELITEA-2222
title: "[EliteaAI/elitea_issues#5294] Status Indicator Accuracy — Verify status reflects auth state"
priority: high
type: functional
module: mcp-servers
status: ready
execution_type: manual
tags: [issue:5294, r-2.0.5, feat:mcp-remote, eng:backend, eng:frontend, nfr:usability, logout-button, mcp-auth]
requirements: [EliteaAI/elitea_issues#5294]
---

# ELITEA-2222: [EliteaAI/elitea_issues#5294] Status Indicator Accuracy

**Module:** Mcp Servers · **Priority:** High · **Type:** Functional

**Objective:** Verify that the MCP status indicator (button or badge) accurately reflects the current authentication state across all three display areas: Chat, Agent-in-Chat, and Agent configuration.

## Preconditions

- Logged in to ELITEA ({{base_url}})
- A preconfigured Remote MCP is added to a Chat conversation
- The same MCP is used in an Agent, which is then added to a Chat conversation
- The MCP toolkit appears in all three locations: Chat, Agent-in-Chat interface, and Agent configuration page
- Status indicator is visible for the MCP in all three locations

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat with direct MCP participant. Observe the MCP status indicator. | Status indicator displays "Authenticated" (or similar) with visual indicator (green dot, check icon). |
| 2 | In the same Chat conversation, add an Agent that has the MCP as a toolkit. Use the Agent in chat. | Chat shows Agent-in-Chat interface; MCP status indicator visible in Agent toolbar. |
| 3 | Observe the MCP status in Agent-in-Chat interface. | Status indicator shows "Authenticated" (matches the direct Chat indicator). |
| 4 | Navigate to Agent configuration page (Agents → [Agent name]). Observe MCP toolkit status. | Status indicator shows "Authenticated". |
| 5 | Click Logout button in any of the three locations (Chat, Agent-in-Chat, or Agent configuration). | Logout succeeds. |
| 6 | Verify all three locations update simultaneously: status changes to "Unauthenticated" (or similar). | All three status indicators show "Unauthenticated" without requiring page refresh. |
| 7 | Click Login button in one location (e.g., Chat). Complete the authentication flow. | Authentication succeeds. |
| 8 | Without navigating, check the status in the other two locations (Agent-in-Chat and Agent config). | All three status indicators update to "Authenticated" immediately or within a few seconds. |

## Expected Final State

- Status indicator accurately reflects authenticated/unauthenticated state
- Status updates are consistent across Chat, Agent-in-Chat, and Agent configuration
- Status updates are immediate (no manual refresh required)

## Pass/Fail Criteria

**Pass:** Status indicator shows correct state in all three locations; updates are consistent and timely.  
**Fail:** Status indicator inconsistent between locations; fails to update after login/logout; shows stale state; requires page refresh to update.
