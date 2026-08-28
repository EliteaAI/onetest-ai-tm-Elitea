---
id: ELITEA-2933
title: "Pipeline Pipeline node: nested sub-pipeline's Toolkit node auth surfaces correctly through the nesting boundary"
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
- A parent pipeline exists containing a Pipeline node that invokes a sub-pipeline
- The sub-pipeline contains a Toolkit node calling a delegated toolkit with no valid token

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Pipeline structure | Parent pipeline → Pipeline node → sub-pipeline → Toolkit node (auth required) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Run the parent pipeline | Run starts and eventually enters the Pipeline node, which invokes the sub-pipeline |
| 2 | Observe the run when the sub-pipeline reaches its Toolkit node | Run pauses; "Toolkit Authorization Required" popup surfaces correctly through the nesting boundary, attributed to the correct sub-pipeline/node |
| 3 | Click **Authorize** and complete OAuth | Toolkit node's tool call executes within the sub-pipeline |
| 4 | Observe parent pipeline continuation | Sub-pipeline completes, control returns to the Pipeline node, and the parent pipeline proceeds correctly |

## Expected Final State

The authorization requirement inside a nested sub-pipeline's Toolkit node surfaces correctly at the top level with accurate attribution, and once resolved, both sub-pipeline and parent pipeline complete correctly.

## Pass/Fail Criteria

**Pass:**
- Popup surfaces correctly despite the nesting, with accurate attribution to the sub-pipeline/node
- After authorization, both sub-pipeline and parent pipeline complete correctly

**Fail:**
- Popup fails to surface, or is misattributed (e.g. shown as the parent pipeline's own node)
- Parent pipeline does not correctly resume after the nested authorization resolves
