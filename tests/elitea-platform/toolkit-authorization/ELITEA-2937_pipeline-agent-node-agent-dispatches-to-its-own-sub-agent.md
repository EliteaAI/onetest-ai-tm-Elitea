---
id: ELITEA-2937
title: "Pipeline Agent node: agent dispatches to its own sub-agent whose toolkit requires auth, and popup attributes the sub-agent specifically"
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
- A pipeline contains an Agent node whose agent has a sub-agent attached
- The sub-agent has a delegated toolkit with no valid token, and the parent agent's routing logic dispatches to that sub-agent

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Pipeline structure | Agent node (parent agent) → dispatches to sub-agent → sub-agent's delegated toolkit (auth required) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Run the pipeline with input that causes the parent agent to dispatch to its sub-agent | Parent agent dispatches; sub-agent begins execution |
| 2 | Observe the run when the sub-agent's toolkit requires auth | Run pauses; "Toolkit Authorization Required" popup appears, attributing the request specifically to the sub-agent (not the parent agent or a generic node) |
| 3 | Click **Authorize** and complete OAuth | Sub-agent's toolkit call executes |
| 4 | Observe pipeline continuation | Sub-agent completes and returns control to the parent agent, which completes, and the pipeline continues correctly |

## Expected Final State

The authorization popup correctly and specifically attributes the requirement to the sub-agent (distinct from the parent agent), and the pipeline resumes correctly through both the sub-agent and parent agent layers after authorization.

## Pass/Fail Criteria

**Pass:**
- Popup attribution specifically names/identifies the sub-agent, not the parent agent generically
- Pipeline correctly resumes through both agent layers after Authorize

**Fail:**
- Popup attributes the request to the parent agent instead of the actual sub-agent
- Pipeline fails to resume correctly through the sub-agent → parent agent chain
