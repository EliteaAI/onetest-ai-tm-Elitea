---
id: ELITEA-1240
title: "SharePoint Login Prompt in Chat — Token Missing/Expired Triggers OAuth Flow"
priority: high
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [int:sharepoint, qachk:4617, r-2.0.2, oauth, chat, p1]
requirements: [EliteaAI/elitea_issues#4335, EliteaAI/elitea_issues#4617]
---
# ELITEA-1240: SharePoint Login Prompt in Chat — Token Missing/Expired Triggers OAuth Flow

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify that when an Agent with a SharePoint toolkit is used in Chat and the token is missing or expired, a login prompt appears inline in the Chat interface. Clicking the login prompt should trigger Microsoft OAuth authentication flow, and upon successful authentication, the pending SharePoint tool call should execute and return results.

## Preconditions

Logged into {{base_url}} as a private project user
Agent configured with SharePoint toolkit (Delegated auth) with no valid token or expired token
Agent has at least one SharePoint tool enabled (e.g., "Get files list", "Search index")
Browser pop-ups are not blocked

## Test Data

Agent: Any agent with SharePoint Delegated toolkit attached (e.g., "SharePoint Assistant")
Prompt: "List the files in the SharePoint documents library"
SharePoint site: Valid SharePoint site URL configured in toolkit credentials
Environment: {{base_url}}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat page | Chat interface opens successfully |
| 2 | Select the agent with SharePoint toolkit attached | Agent is selected, chat input is ready |
| 3 | Send the prompt: 'List the files in the SharePoint documents library' | Agent begins processing, SharePoint tool is invoked |
| 4 | Observe the Chat interface for login prompt | A 'Login' button/prompt appears inline in the Chat (similar to Remote MCP login pattern), NOT a silent error |
| 5 | Click the Login button/prompt in Chat | Microsoft OAuth popup or redirect opens to login.microsoftonline.com |
| 6 | Complete OAuth login with valid Microsoft credentials | OAuth popup closes automatically, returns to Chat |
| 7 | Observe Chat response without manual refresh | The pending SharePoint tool call executes successfully and returns a file listing in the chat response |
| 8 | Verify no authentication errors appear | No 401/403 errors, tool execution completes normally |

## Expected Final State

No 401/403 errors, tool execution completes normally

## Pass/Fail Criteria

PASS:
- Login prompt appears inline in Chat when token is missing/expired
- Clicking Login opens Microsoft OAuth flow (popup/redirect)
- After successful OAuth, Chat does NOT require manual refresh
- SharePoint tool executes and returns valid results (file list or empty-but-successful response)

FAIL:
- No login prompt appears (silent failure or generic error)
- Login prompt appears but clicking it does nothing
- OAuth completes but tool still fails with authentication error
- Page requires manual refresh to see results
