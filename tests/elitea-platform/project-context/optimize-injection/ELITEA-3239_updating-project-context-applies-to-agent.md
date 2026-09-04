---
id: ELITEA-3239
title: "Updating Project Context Applies to New Agent Requests"
priority: critical
type: functional
module: project-context
status: draft
execution_type: manual
tags: [project-context, agents, r-2.0.6, eng:optimization]
requirements: [EliteaAI/elitea_issues#5326]
---

## Preconditions

- User is logged in to `{{base_url}}`
- 
- Agent with "Ignore Project Context" = OFF
- Initial Project Context: `Environment: staging`

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/<project>/agents/<agent>` |
| Initial Context | `Environment: staging` |
| Updated Context | `Environment: production` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Set Project Context to "Environment: staging" | Context saved |
| 1 | Run agent with prompt: "What environment are we in?" | Agent responds: "staging" |
| 2 | Update Project Context to "Environment: production" | Context updated |
| 3 | Run agent **again** with same prompt: "What environment are we in?" | Agent responds: "production" (updated context applied) |
| 4 | Verify no caching issues causing stale context | Agent consistently uses updated context |

## Expected Final State

Updated Project Context applies to new agent executions. Optimization preserves context update propagation for agents.

## Pass/Fail Criteria

**Pass:**
- Initial context applied correctly to agent
- Updated context applied to subsequent agent runs
- No stale context served
- Context update immediate and consistent

**Fail:**
- Updated context not applied to agent
- Stale context served after update
- Caching issues prevent context update
- Errors after context update
