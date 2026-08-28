---
id: ELITEA-2930
title: "Pipeline Toolkit node: single node calling an OAuth-requiring toolkit pauses and resumes the pipeline run correctly"
priority: high
type: integration
module: toolkit-authorization
status: draft
execution_type: manual
tags: [feat:mcp-remote, feat:toolkits, int:openapi, int:sharepoint, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6072]
---

## Preconditions

- User is logged in to `{{base_url}}`
- A pipeline exists containing a single Toolkit node (a node that calls a toolkit directly, not via an agent) calling a SharePoint/OpenAPI toolkit whose credential is delegated/interactive, with no valid token
- The pipeline is runnable via the Test Panel or as a chat participant

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Pipeline structure | Single Toolkit node → downstream node consuming its output |
| Toolkit | SharePoint (Delegated), no valid token |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Run the pipeline via the Test Panel or a chat conversation where the pipeline is a participant | Pipeline run starts |
| 2 | Observe the run at the Toolkit node | Run pauses at the Toolkit node; "Toolkit Authorization Required" popup appears, correctly attributed to the pipeline/node (not misattributed to an agent) |
| 3 | Click **Authorize** and complete OAuth | Toolkit node's tool call executes |
| 4 | Observe pipeline continuation | Pipeline continues to any downstream nodes, correctly using the Toolkit node's output |

## Expected Final State

The pipeline pauses precisely at the Toolkit node requiring auth, correctly attributes the popup to the pipeline/node, and resumes execution automatically after Authorize, with downstream nodes correctly consuming the Toolkit node's output.

## Pass/Fail Criteria

**Pass:**
- Pipeline run pauses at the Toolkit node and popup is attributed to the pipeline/node
- After Authorize, the Toolkit node executes and the pipeline continues correctly

**Fail:**
- Popup is misattributed to an agent rather than the pipeline/Toolkit node
- Pipeline fails to resume or downstream nodes do not receive the correct output after authorization
