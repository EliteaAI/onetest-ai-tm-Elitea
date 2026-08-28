---
id: ELITEA-2936
title: "Pipeline Agent node: single agent node's toolkit requiring auth pauses and resumes the pipeline correctly"
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
- A pipeline contains a single Agent node whose agent has a delegated toolkit (SharePoint/OpenAPI/Remote MCP) with no valid token

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Pipeline structure | Single Agent node (agent has a delegated toolkit requiring auth) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Run the pipeline | Run enters the Agent node; the agent invokes its toolkit |
| 2 | Observe the run when the agent's toolkit requires auth | Run pauses; "Toolkit Authorization Required" popup appears, correctly attributed to the Agent node/agent |
| 3 | Click **Authorize** and complete OAuth | The agent's toolkit call executes |
| 4 | Observe pipeline continuation | Pipeline continues past the Agent node, correctly using the agent's output |

## Expected Final State

The pipeline pauses at the Agent node when its toolkit requires auth, correctly attributes the popup to that agent, and resumes automatically after Authorize with correct downstream continuation.

## Pass/Fail Criteria

**Pass:**
- Popup correctly attributed to the Agent node/agent whose toolkit needs auth
- Pipeline resumes and continues correctly after Authorize

**Fail:**
- Popup is unattributed or misattributed (e.g. shown as a generic Toolkit node)
- Pipeline fails to resume or produces incorrect output after authorization
