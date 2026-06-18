---
id: ELITEA-1239
title: "SharePoint Toolkit in Pipeline Node — OAuth Login and Execution"
priority: high
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [int:sharepoint, qachk:4617, pipeline, r-2.0.2, oauth, p1]
requirements: [EliteaAI/elitea_issues#4335, EliteaAI/elitea_issues#4617]
---
# ELITEA-1239: SharePoint Toolkit in Pipeline Node — OAuth Login and Execution

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify that when SharePoint toolkit is used within a Pipeline node and the token is missing or expired, the SharePoint login button appears in the Pipeline node configuration or during execution, OAuth flow completes successfully, and the Pipeline execution proceeds with SharePoint tool calls executing correctly.

## Preconditions

Logged into {{base_url}} as a private project user
Pipeline exists with a node that uses SharePoint toolkit (e.g., Agent node with SharePoint toolkit, or Toolkit node with SharePoint)
SharePoint toolkit has Delegated auth configured with no valid token
Browser pop-ups are not blocked

## Test Data

Pipeline: "Document Processing Pipeline"
Node: Agent node or Toolkit node with SharePoint toolkit attached
SharePoint toolkit: Delegated auth, status "Not Connected"
SharePoint site: Valid SharePoint site URL configured in toolkit credentials
Test input: Any input that triggers SharePoint tool execution (e.g., "List SharePoint files")
Environment: {{base_url}}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Pipelines page and open the Pipeline with SharePoint toolkit node | Pipeline canvas opens, SharePoint toolkit node is visible |
| 2 | Click on the node using SharePoint toolkit to view configuration | Node configuration panel opens |
| 3 | Observe if Login button appears in node configuration (if toolkit status is visible) | If toolkit status is shown, 'Not Connected' status and Login button should be visible in node config or toolkit panel |
| 4 | If Login button is visible in config, click it and complete OAuth | Microsoft OAuth popup opens, login completes, status updates to 'Logged in' |
| 5 | If Login button is NOT in config, proceed to run the Pipeline | Pipeline execution starts |
| 6 | When Pipeline reaches SharePoint node with missing token, observe behavior | Pipeline execution pauses or displays Login prompt/button in execution UI or Pipeline Chat |
| 7 | Click Login button (in execution UI or Pipeline Chat) | Microsoft OAuth popup opens to login.microsoftonline.com |
| 8 | Complete OAuth login with valid credentials | OAuth popup closes, returns to Pipeline |
| 9 | Observe Pipeline execution continuation | Pipeline proceeds after authentication, SharePoint tool executes successfully |
| 10 | Verify Pipeline output includes SharePoint data (file list, search results, etc.) | Pipeline completes successfully, output contains expected SharePoint data without authentication errors |

## Expected Final State

Pipeline completes successfully, output contains expected SharePoint data without authentication errors

## Pass/Fail Criteria

PASS:
- Login button appears in Pipeline node config or during execution when token is missing
- Clicking Login opens Microsoft OAuth flow
- After successful OAuth, Pipeline execution proceeds without manual restart
- SharePoint tool executes successfully within Pipeline
- Pipeline output contains expected SharePoint data

FAIL:
- No login button appears in node config or during execution (silent failure)
- Login button appears but does nothing when clicked
- OAuth completes but Pipeline still fails with authentication error
- Pipeline requires manual restart/re-run after authentication
