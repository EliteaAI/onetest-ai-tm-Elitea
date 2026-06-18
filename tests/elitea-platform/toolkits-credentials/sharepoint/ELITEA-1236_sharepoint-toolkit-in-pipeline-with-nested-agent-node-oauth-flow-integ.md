---
id: ELITEA-1236
title: "SharePoint Toolkit in Pipeline with Nested Agent Node — OAuth Flow Integration"
priority: medium
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [int:sharepoint, agent-node, qachk:4617, sub-agent, pipeline, r-2.0.2, nested, oauth, p2]
requirements: [EliteaAI/elitea_issues#4335, EliteaAI/elitea_issues#4617]
---
# ELITEA-1236: SharePoint Toolkit in Pipeline with Nested Agent Node — OAuth Flow Integration

**Module:** Sharepoint · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when a Pipeline contains an Agent node that uses SharePoint toolkit, and that Agent itself has a sub-agent with SharePoint tools, the OAuth login flow works correctly during Pipeline execution. Login should be triggered appropriately, and both Agent and Sub-Agent SharePoint calls should execute successfully.

## Preconditions

Logged into {{base_url}} as a private project user
Sub-Agent exists with SharePoint toolkit (Delegated auth) attached, no valid token
Parent Agent exists with Sub-Agent configured and also has SharePoint toolkit attached
Pipeline exists with an Agent node using the Parent Agent
Browser pop-ups are not blocked

## Test Data

Sub-Agent: "SharePoint File Reader" (SharePoint toolkit, "Get files list" enabled)
Parent Agent: "Document Processor" (has "SharePoint File Reader" as sub-agent, also has SharePoint toolkit for own use)
Pipeline: "Document Analysis Pipeline" (contains Agent node with "Document Processor")
SharePoint site: Valid SharePoint site URL configured in both toolkit credentials
Pipeline input: "Process SharePoint documents using all available tools"
Environment: {{base_url}}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Verify Pipeline structure: contains Agent node with Parent Agent that has Sub-Agent with SharePoint | Pipeline has correct structure, both agents have SharePoint toolkits in 'Not Connected' state |
| 2 | Navigate to Pipelines page and open the Pipeline | Pipeline canvas opens with Agent node visible |
| 3 | Run the Pipeline with input: 'Process SharePoint documents using all available tools' | Pipeline execution starts, reaches Agent node |
| 4 | Observe behavior when Agent node invokes Parent Agent with SharePoint toolkit | Login prompt appears in Pipeline Chat or execution UI when Parent Agent attempts SharePoint call |
| 5 | Click Login button and complete OAuth for Parent Agent's SharePoint toolkit | OAuth completes successfully, Parent Agent's SharePoint call executes |
| 6 | Observe behavior when Parent Agent invokes Sub-Agent with SharePoint toolkit | If Sub-Agent SharePoint token is also missing, another Login prompt appears (or same token is reused if same toolkit instance) |
| 7 | Complete OAuth for Sub-Agent's SharePoint toolkit if prompted | OAuth completes, Sub-Agent's SharePoint call executes |
| 8 | Verify Pipeline execution continues through all nodes after authentication | Pipeline completes successfully without manual restart or additional authentication prompts |
| 9 | Check Pipeline output for SharePoint data from both Agent and Sub-Agent calls | Pipeline output contains SharePoint data from both levels (Parent Agent and Sub-Agent SharePoint tool calls) |
| 10 | Verify no authentication errors or broken invocation chains | No 401/403 errors, Agent -> Sub-Agent chain intact, Pipeline execution successful |

## Expected Final State

No 401/403 errors, Agent -> Sub-Agent chain intact, Pipeline execution successful

## Pass/Fail Criteria

PASS:
- Login prompt appears during Pipeline execution when Agent or Sub-Agent needs SharePoint authentication
- OAuth flow completes successfully for all required authentication levels
- Pipeline execution continues automatically after authentication (no manual restart)
- SharePoint tool calls execute successfully in both Parent Agent and Sub-Agent contexts
- Pipeline output contains SharePoint data from all levels
- No authentication errors or broken invocation chains

FAIL:
- No login prompt appears during Pipeline execution (silent failure)
- OAuth completes but Pipeline still fails with authentication error
- Pipeline requires manual restart after authentication
- Agent -> Sub-Agent invocation chain breaks
- SharePoint tool calls fail despite successful authentication
- Pipeline output is missing expected SharePoint data from any level
