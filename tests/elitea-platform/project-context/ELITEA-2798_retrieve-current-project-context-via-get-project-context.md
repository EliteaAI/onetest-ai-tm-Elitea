---
id: ELITEA-2798
title: "Retrieve current project context via get_project_context"
priority: high
type: functional
module: project-context
status: ready
execution_type: manual
tags: [feat:chat, story:6239, r-2.0.6, project-context-builder, tool:get_project_context]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-2798: Retrieve current project context via get_project_context

## Preconditions

- Test project (project_id 13) is accessible
- Project 13 has an existing project context configured

## Test Data

| Field | Value |
|-------|-------|
| Request payload | `{"project_id": 13}` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Call get_project_context with `{"project_id": 13}` | Response returns the current `content` and `enabled` fields, matching the stored configuration |

## Expected Final State

The current project context content and enabled state are returned accurately for a valid project.

## Pass/Fail Criteria

**Pass:**
- `content` and `enabled` returned correctly and match stored state

**Fail:**
- Missing fields, stale data, or an error is returned for a valid project
