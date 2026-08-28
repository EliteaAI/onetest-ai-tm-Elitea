---
id: ELITEA-2938
title: "Pipeline Agent node: agent with multiple toolkits requires sequential auth inside a pipeline run"
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
- A pipeline contains an Agent node whose agent has two or more delegated toolkits attached (e.g. SharePoint + OpenAPI), none with a valid token
- The agent's task requires it to call both toolkits during the run

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Pipeline structure | Single Agent node, agent has 2+ delegated toolkits, both required for the task |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Run the pipeline with input requiring the agent to use both toolkits | Agent begins execution; the first toolkit call triggers a popup |
| 2 | Authorize the first toolkit's popup | First toolkit call executes; agent proceeds to call the second toolkit |
| 3 | Observe and Authorize the second toolkit's popup | Second toolkit call executes |
| 4 | Observe agent/pipeline completion | Agent completes its task using both toolkits' results, and the pipeline continues correctly |

## Expected Final State

Both toolkit authorizations for the same agent are surfaced and resolved sequentially and correctly, and the agent/pipeline completes using both toolkits' results.

## Pass/Fail Criteria

**Pass:**
- Both toolkit popups for the same agent are surfaced in sequence, each correctly attributed
- Agent/pipeline completes using both toolkits' outputs after both are authorized

**Fail:**
- One toolkit's popup is skipped, merged with the other, or never surfaces
- Agent/pipeline completes without correctly incorporating both toolkits' results
