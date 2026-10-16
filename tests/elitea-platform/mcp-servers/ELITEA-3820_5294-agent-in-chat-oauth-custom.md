---
id: ELITEA-3820
title: "[EliteaAI/elitea_issues#5294] Chat Using Agent with Toolkit: Login/Logout Auth Flow"
priority: high
type: functional
module: mcp-servers
status: ready
execution_type: manual
tags: [issue:5294, r-2.0.5, feat:mcp-remote, eng:backend, eng:frontend, nfr:usability, logout-button, mcp-auth, agent-in-chat]
requirements: [EliteaAI/elitea_issues#5294]
---

# ELITEA-3820: [EliteaAI/elitea_issues#5294] Chat Using Agent with Toolkit: Login/Logout Auth Flow

**Module:** Mcp Servers · **Priority:** High · **Type:** Functional

**Objective:** Verify that login and logout flows work correctly for MCPs in Agent-in-Chat interface, supporting OAuth 2.0 and Custom Headers authentication types.

## Preconditions

- Logged in to ELITEA ({{base_url}})
- Two Agents configured: one with OAuth 2.0 MCP toolkit, one with Custom Headers MCP toolkit
- Both Agents initially in unauthenticated state for their respective MCPs
- Chat conversation open with ability to invoke Agents

## Test Data

| Agent | Auth Type | Credentials |
|-------|-----------|-------------|
| Agent A | OAuth 2.0 | Valid client_id, client_secret |
| Agent B | Custom Headers | Valid header names and values |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | In Chat, invoke Agent A (OAuth 2.0 MCP toolkit). Agent-in-Chat interface opens. | Agent-in-Chat interface loads; MCP toolbar visible. |
| 2 | Observe Agent A's MCP toolbar. Verify login button is visible (unauthenticated). | Login button visible; logout button hidden. |
| 3 | Click Login button on MCP toolbar in Agent-in-Chat. Complete OAuth 2.0 flow. | OAuth 2.0 authorization succeeds; access token obtained. |
| 4 | Verify Agent A's MCP toolbar updates: logout button now visible. | Logout button visible; authenticated state shown. |
| 5 | Click Logout button on MCP toolbar. | Logout succeeds; login button visible again. |
| 6 | Close Agent A (return to Chat). Invoke Agent B (Custom Headers MCP toolkit). | Agent B-in-Chat interface opens. |
| 7 | Observe Agent B's MCP toolbar. Verify login button visible (unauthenticated). | Login button visible; logout button hidden. |
| 8 | Click Login button; enter custom header values when prompted. | Custom headers stored successfully. |
| 9 | Verify Agent B's MCP toolbar: logout button now visible. | Logout button visible; authenticated state shown. |
| 10 | Click Logout button on MCP toolbar. | Logout succeeds; login button visible again. |

## Expected Final State

- Both OAuth 2.0 and Custom Headers auth flows work in Agent-in-Chat
- UI updates reflect authentication state changes
- Login/logout cycles complete without errors
- No cross-contamination between Agent A and Agent B authentication states

## Pass/Fail Criteria

**Pass:** Both auth types login/logout successfully in Agent-in-Chat; UI updates correctly.  
**Fail:** Either auth type fails; UI does not update; logout does not clear credentials.
