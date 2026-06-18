---
id: ELITEA-1216
title: "SharePoint Toolkit — Pipeline Node with /teams/ Site Path Executes Without Errors"
priority: high
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [feat:toolkits, feature:2584, r-2.0.4]
requirements: [EliteaAI/elitea_issues#2584]
---
# ELITEA-1216: SharePoint Toolkit — Pipeline Node with /teams/ Site Path Executes Without Errors

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify that a Pipeline containing a SharePoint toolkit node configured with Site Path teams/TestTeam executes successfully and returns data from the /teams/ space. Covers: Pipeline execution with SharePoint node; node output contains /teams/ data; no errors in execution logs.

## Preconditions

- Logged in to ELITEA at {{base_url}}
- SharePoint toolkit with Site Path teams/TestTeam, Get files list tool enabled
- A Pipeline with a SharePoint toolkit node using that toolkit configured (tool = Get files list)
- /teams/TestTeam site accessible with at least one file

## Test Data

Site Path: teams/TestTeam
Pipeline node tool: Get files list

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Pipelines and open the Pipeline containing the SharePoint node. Verify the node uses the toolkit with Site Path teams/TestTeam. | Pipeline editor loads. SharePoint node is visible with correct toolkit. |
| 2 | Execute the Pipeline. | Pipeline run starts. No immediate error before node execution. |
| 3 | Wait for execution to complete. Inspect the SharePoint node output. | Node output contains file data from the /teams/TestTeam site. |
| 4 | Open the Pipeline execution logs. | No error entries related to SharePoint site resolution. No HTTP 4xx/5xx logged. |

## Expected Final State

No error entries related to SharePoint site resolution. No HTTP 4xx/5xx logged.

## Pass/Fail Criteria

Pass:
- Pipeline executes to completion without errors
- SharePoint node output contains data from the /teams/ space
- No error entries in execution logs

Fail:
- Pipeline fails at the SharePoint node
- Node output is empty or contains an error referencing a wrong site
- Execution logs show HTTP 4xx/5xx or 'site not found' for the SharePoint node
