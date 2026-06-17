---
id: ELITEA-1238
title: "SharePoint Toolkit in Nested Sub-Agent Structure — OAuth Login Propagates Correctly"
priority: high
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [int:sharepoint, qachk:4617, sub-agent, r-2.0.2, nested, oauth, p1]
requirements: [EliteaAI/elitea_issues#4335, EliteaAI/elitea_issues#4617]
---
# ELITEA-1238: SharePoint Toolkit in Nested Sub-Agent Structure — OAuth Login Propagates Correctly

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify that when SharePoint toolkit is used within a nested sub-agent structure (Parent Agent -> Sub-Agent -> SharePoint toolkit), the OAuth login prompt surfaces correctly in Chat, authentication completes successfully, and the SharePoint tool call executes without breaking the sub-agent invocation chain.

## Preconditions

Logged into {{base_url}} as a private project user
Sub-Agent exists with SharePoint toolkit (Delegated auth) attached, with no valid token
Parent Agent exists with the Sub-Agent configured as a tool/sub-agent
Browser pop-ups are not blocked

## Test Data

Sub-Agent: "SharePoint Helper" with SharePoint toolkit and at least one SharePoint tool enabled
Parent Agent: "Document Manager" with "SharePoint Helper" as a sub-agent/tool
SharePoint site: Valid SharePoint site URL configured in toolkit credentials
Prompt: "Use SharePoint Helper to list all documents in the library"
Environment: {{base_url}}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agents page and verify Parent Agent has Sub-Agent configured | Parent Agent configuration shows Sub-Agent in tools/sub-agents list |
| 2 | Verify Sub-Agent has SharePoint toolkit attached with no valid token | Sub-Agent configuration shows SharePoint toolkit, toolkit status is 'Not Connected' |
| 3 | Navigate to Chat and select the Parent Agent | Chat opens with Parent Agent selected |
| 4 | Send prompt: 'Use SharePoint Helper to list all documents in the library' | Parent Agent begins processing, invokes Sub-Agent |
| 5 | Observe Chat for login prompt when Sub-Agent attempts to use SharePoint toolkit | Login prompt appears inline in Chat (not hidden or lost in sub-agent context) |
| 6 | Click the Login button in Chat | Microsoft OAuth popup opens to login.microsoftonline.com |
| 7 | Complete OAuth login with valid credentials | OAuth popup closes, returns to Chat |
| 8 | Observe Chat response | Sub-Agent's SharePoint tool call executes successfully, Parent Agent receives results and displays file listing in chat |
| 9 | Verify the sub-agent invocation chain did not break | No sub-agent invocation errors, full response chain is visible in Chat (Parent -> Sub-Agent -> SharePoint tool -> results) |

## Expected Final State

No sub-agent invocation errors, full response chain is visible in Chat (Parent -> Sub-Agent -> SharePoint tool -> results)

## Pass/Fail Criteria

PASS:
- Login prompt appears in Chat when Sub-Agent attempts to use SharePoint toolkit
- OAuth flow completes successfully
- SharePoint tool executes within Sub-Agent context
- Parent Agent receives and displays Sub-Agent results correctly
- No sub-agent invocation errors or broken response chain

FAIL:
- Login prompt does not appear (silent failure in sub-agent context)
- OAuth completes but sub-agent invocation fails
- SharePoint tool fails with authentication error despite successful login
- Response chain breaks (Parent Agent loses Sub-Agent context or results)
